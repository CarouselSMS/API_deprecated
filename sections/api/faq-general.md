FAQ - general
=============

How do I receive messages from phones? Do I need to poll the Service Layer (using websockets, etc.)?
----------------------------------------------------------------------------------------------------

If you have an application that you want to accept incoming messages,
all you need to do is to give us (register on your application page) the
URL you’d like us to call when they arrive. The response will be in the
form of a POST request containing all of the message details. Moreover,
you can even respond with the text to send back to that phone as a reply
if you’d like.

So, no, you don’t need to poll our system for new messages. Simply write
a handler that accepts POST requests and do whatever your business logic
requires with it. This handler will receive other events as well
(subscriptions, delivery reports, etc.), but you are free to implement
only the parts you need. For details, consult with the Callbacks
documentation.

Sending Messages to Phones
--------------------------

### Single message to a single number

When you want to deliver a message to a single phone number, use the
`send_message` API call, specifying the message body, phone number,
whether the response is expected, and the time of delivery if you’d like
to schedule it to be sent later.

### Single message to several numbers

When you have something to say to several phone numbers, you can use the
`send_message` API call as you would with a the single phone number
(above), but specify all of your numbers as a comma-separated list.

### Custom messages to several numbers

When you want to send a personalized message that follows a common
pattern to several numbers, you can do that with the `send_messages`
API call. Just specify the template, like `"Hello {{name}}"`, and then
provide a JSON-formatted hash of phone numbers to the substitutions map, like `"{’0123456789’: {’name’: ‘Jack’}, …}"`. We will place your custom
values for each number in the corresponding placeholders and deliver.

### How do I get the delivery status for the message?

When you send a message, we return the ID of this message that you could
use for your internal records, and for asking for the delivery status of
the message. Even though you will be notified through the callback when
the status of the message changes, you can still ask the Service Layer
for the status directly at any moment.

### What are the delivery statuses?

When the delivery status is reported or you get it back as the result of
your direct query, it can be one of the following values:

-   `0` -- Message is still in the queue and was not pushed to the mobile
    provider for delivery. This can happen when you’ve submitted the
    message for the future delivery or when the mobile provider hasn’t
    confirmed the reception of the message from us. The latest happens
    sometimes because of the asynchronous nature of the messaging.
    Nothing to worry about.
-   `1` -- Message was successfully delivered to the phone.
-   `2` -- Message was not delivered to the phone. It’s either unsupported
    carrier, land line or the phone has text messaging disabled.
-   `4` -- Message is queued for the delivery on the mobile provider side.
    Sometimes people have no reception, their phones are off or the
    network is overloaded. The mobile provider reports that the message
    is received from us and that it’s in the queue for delivery. There
    will be another status update after that soon.

Sessions
--------
### What is a session and why is it important?

We have one shortcode and several applications. When a message from a
cell phone arrives, it’s the Service Layer’s responsibility to identify
which application to send this message to. The Service Layer maintains
the table of sessions (virtual links with phone numbers and
applications). If there’s a record for the cell phone number in
question, it knows the application to send the message body to.

Once a user is in session with your application, you can treat the
shared shortcode as thought it were dedicated, with a wide-open keyword
space. For instance, if you’re building a chat application, there’s no
need for your users to memorize strange commands, like “*reply to every
message with MYCHATKEYWORD then your message*,” to send in free-form
messages. Just initiate a session and let them text naturally.

### How are sessions established?

If there’s no record in the sessions table, the Service Layer takes the
body of the message and attempts to find an application that is
expecting something resembling that message body. For example, when your
application is associated with the keyword `Surf`, when a message with
this text arrives, the Service Layer will establish a virtual link
between the source phone number and your application. All of the
following messages (no matter the content) from this phone number will
be sent directly to your application until the session expires (based on
inactivity type) or until the phone number sends an opt-out message,
such as `STOP`.

Keywords
--------
### What are keywords?

Traditionally (insofar as SMS has traditions), keywords were the primary
means of interacting with a text-messaging system. You would set up a
simple marketing campaign and have users subscribe to it by texting in a
keyword to a shortcode, or set up an auto-responder to kick back a
coupon when a user texts in a particular keyword.

With our API, keywords are used to identify which application a user
intends to talk to. Any application can have multiple keyword
associations. All keywords can be matched in either `Starts with` or `Matches exactly` modes. We treat keywords as only the starting point
for a truly functional SMS application.

### Why do I need keywords?

If your app has no keywords associated with it, we won’t be able to
route any messages to it. When a message from a phone number with no
active session comes, we scan it for keywords and see which application
matches, create a session for it and send the message over. If you don’t
have keywords, your app will never be matched, and your users will be
shouting into the ether.

### What are the `Starts with` and `Matches exactly` modes?


`Starts with` mode matches any keywords a user texts in that begin with
the keyword you associate. For example, if you have a weather
forecasting application, you may want to associate the keyword
**Forecast** and set the mode to `Starts with`. That will allow your users
to send messages like **Forecast Miami, Florida**. The Service Layer will
see your target keyword at the beginning, establish a
session and send the whole message to your application
for processing.

`Matches exactly` mode is used when the message is supposed to contain
*only* the target keyword. It can have spaces and letters in mixed
cases, but only this keyword will match and your application will be
selected.

Note that keywords are case insensitive. Talk to us if you need more
advanced tools, like RegEx-generated keywords.

### What are the `Auto-subscribe` and `Auto-subscribe Tags`?

If you have Subscription Module enabled for your application, you can
make it so that when a particular keyword is recognized, the user is
also automatically subscribed. If you specify the list of tags, they
will be used to tag the user when being subscribed through this keyword.
Remember, that you can send messages to the users with certain tags, so
it’s a flexible way to organize your subscribers list.

### What is `Don’t start session`?

Imagine that you have an app that just sends one-off responses, like
weather forecasts for a given area or time table information for a given
station. You don’t need to maintain a persistent session between the
user and the application.

Another scenario is when your application sends alerts of different type
and you want to minimize the implementation effort. For different
keywords, you enable the auto-subscription feature (along with the
Subscription Module) and auto-tag the users without creating a session.
Then a user can send several keywords one after another and all you will
need to do is to send messages to your subscribers filtered by tags.

### What is `Auto-response`?

The auto-response is just the text you want your users to receive when
they send you a given keyword. It can be used with other options in
different combinations to achieve stunning effects. In the above
scenario, the auto-response can be used to send confirmations back to
the users saying that you’ve successfully subscribed them to your
alerts.

This feature, however, has a side-effect. If you use the Subscription
Module in your application and the Auto-response for the keyword that
has auto-subscription enabled, your users will receive at least two
messages (the third message could be the First-Timers Message when the
user texts you for the first time) - one for your Auto-response and
another one for the confirmation on successful subscription.

Subscriptions
-------------

### When do I use `send_message` vs. `send_subscription_message`?

There are currently two ways to send messages in the system:

- **Sending a single message to one or more phone numbers.** -- When you
send a message to arbitrary phone numbers, all you need is the text of
the message and the list of phone numbers you want this message to be
delivered to.

- **Sending a message to subscribers.** -- This option is available only if
you use the `Subscription Module` on the Service
Layer side. When you have subscribers, you can send them a message
without listing all of them individually. This is convenient when you
have hundreds or thousands of numbers, and allows you to selectively
send messages to pre-defined groups using our tagging
system.

### How do I put people on the subscribers list using the Subscription Module?

If you intend to use our Subscription Module features, for example, for
sending bulk messages, the only way to put a phone number on the list is
to let them subscribe themselves. You cannot tell the system to add
numbers to the list, as we keep our system compliant with the **Mobile
Marketing Association’s Best Practices**.
Users must go through the full opt-in cycle and confirm that they indeed
want to be subscribed, preventing unsolicited messaging.

### Can I unsubscribe people from the Subscription Module?

Currently, no. Users can only unsubscribe themselves. However, we’ll
consider adding this feature if there’s enough interest.

### What are `tags`?

Tags are used to organize your subscribers in a free-form fashion,
familiar to users of Facebook, Flickr or any number of web applications.
It’s possible to have a flat subscribers list, but you may want to split
it into groups so that you can address each one separately when sending
bulk messages. Tags can be stacked and tagged lists rearranged in an
intuitive, non-hierarchical way. We use these in place of *categories*
and *lists*.

A good use for tagging is A/B testing advertising, especially of any
marketing you do outside of the internet that’s otherwise hard to
measure. For example, you can find out which of several newspapers is
the more cost-effective advertising channel by printing the same ads but
with a different keyword in each of them. Those keywords should have two
tags associated with them: one for the campaign, and another for the
paper it was shown in. You could then measure your opt-in rate against
the number of impressions , and still keep all of your subscribers in
the same common bucket for sending mass texts later.

Tags make it easy to do any kind of layered segmentation.

### How do I tag subscribers?

There are two simple ways to assign tags:

- If you use the Subscription Module), you
will receive a `subscription_created` callback every time someone
subscribes. In the response to this message, you can specify a
comma-separated list of tags to assign to this particular number. The
Service Layer will receive the response and tag your new subscriber as
necessary.

- If you have some existing subscribers and want to tag them, you can
use the `tag_subscribers` API call with the desired tags and the phone
numbers to assign tags to existing numbers.

### How do I untag subscribers?

If, at any point you need to remove tags from some numbers on your
subscriber list, you can use the `untag_subscribers` API call.

Static Responses
----------------

### What are `static responses` used for?

Static Responses let you build a basic SMS
application without writing any code. If all you need is a canned
responses to a given set of keywords, you can enter them through your
application ‘edit’ screen and the Service Layer will automatically send
those back to your users when a matching message arrives. For example,
if you want to send your card to everyone who sends **Jack** to your
application, you could write an application that would receive a message
from the Service Layer, see if it reads **Jack** and respond. But with
Static Responses, you can simply tell the
Service Layer to send your desired text any time it sees incoming
message with the text **Jack**.

### When do Static Responses come into play -- or why doesn’t my Static Response work?

Static Responses are canned responses to
the known client messages. They work exactly as if the message was sent
to your application, recognised and replied with the known text. This
means that in order for the Static
Responses to work, there has to be a
session established between the phone number and your
application first. If there’s no session between the
phone number and your application, we don’t know which application to
send a message to, and thus it never reaches your Static
Responses.

If you’d like to set up simple auto-responders when there’s no session
in place , you can simply set up a keyword with an `auto-response`.

You can find details on how Sessions work in the corresponding
section.

Customizing Module Messages
---------------------------

There are three main modules that work together for the application --
the *Welcome*, *Help* and *Subscription* modules. Each of them has associated
messages that can be customized or left blank. We’ll examine them in the
following sections.

### Welcome Message

Every application can be configured to welcome its new users with a
message. We know when it’s the first time someone texts you and can send
a reply to them automatically, but also give you a chance to provide
your own content. Think of this welcome message as an optional
additional message. Since it’s optional, you can leave it blank if you
don’t need it.

### Help Message

If your response to **HELP** message never changes, you may want to use our
next module -- the **Help Module**. It will send an automatic response to
anyone asking for help. If you leave this message blank, the message
will be sent to your application as any other message.

### Subscription Messages

Here we have two messages that work only when the Subscription Module is
enabled:

- `Subscribe message` -- used to confirm that the user has been subscribed
successfully.
-- `Stop message` -- used to confirm the successful unsubscribing.

Customize these messages to include your store name, and links to your
web site.