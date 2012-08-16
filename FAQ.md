FAQ
===

A list of common questions. Ask a question via pull request or email **ytspar@gmail.com**.

General
-------

### How do I receive messages from phones? Do I need to poll the Service Layer (using websockets, etc.)?

For an application to accept incoming messages, it needs a gateway URL. You can register this URL on your application page. We'll direct all incoming messages to that address. The response will be in the form of a POST request containing all of the message details. You can even respond with a message body to send back to that phone as a reply if you’d like.

So you don’t need to poll our system for new messages. Simply write a handler that accepts POST requests and do whatever your business logic requires with it. This handler will receive other events as well (subscriptions, delivery reports, etc.). You're free to implement only the parts you need. For details, check the [Callbacks
documentation](https://github.com/CarouselSMS/API/blob/master/sections/api/callbacks-general.md).

Sending messages to phones
--------------------------

### Single message to a single number

When you want to deliver a message to a single phone number, use the [`send_message` API call](https://github.com/CarouselSMS/API/blob/master/sections/api/messaging.md), specifying the message body, phone number, whether a response is expected, and, if you'd like the message sent later, specify the time of delivery.

### Single message to several numbers

When you have something to say to several phone numbers, you can use the [`send_message` API call](https://github.com/CarouselSMS/API/blob/master/sections/api/messaging.md) as you would with a the single phone number (see above). But instead of including only one number, specify all of the numbers you'd like the message delivered to as a comma-separated list.

### Custom messages to several numbers

When you want to send a personalized message that follows a common pattern to several numbers, you can do that with the [`send_messages` API call](https://github.com/CarouselSMS/API/blob/master/sections/api/messaging.md). Outline the template, like `"Hello {{name}}"`, and then provide a JSON-formatted hash of phone numbers to the substitutions map, like `"{’0123456789’: {’name’: ‘Jack’}, …}"`. We will place your custom values for each number in the corresponding placeholders and deliver.

### How do I get the delivery status for the message?

When you send a message, we return the ID of this message that you can use for your internal records, and for asking the delivery status of the message. Even though you will be notified through the callback when the status of the message changes, you can still ask the Service Layer for the status directly at any moment.

### What are the delivery statuses?

When the delivery status is reported or you get it back as the result of your direct query, it will be one of the following values:

-   `0` -- Message is still in the queue and was not pushed to the mobile
    provider for delivery. This can happen when you’ve submitted the
    message for the future delivery or when the mobile provider hasn’t
    confirmed that they've received the message from us. The latter happens
    periodically due to the asynchronous nature of SMS.
    Nothing to worry about.
-   `1` -- Message was successfully delivered to the gateway and subsequently, the phone.
-   `2` -- Message was not delivered to the gateway or phone. Likely causes: either an unsupported
    carrier, land line or the phone has text messaging disabled.
-   `4` -- Message is queued for delivery on the mobile provider side.
    Sometimes recipients have no reception, their phones are off or the
    network is overloaded. The mobile provider reports that the message
    is received from us and that it’s in the queue for delivery. There
    will be another status update soon after this one.

Sessions
--------

### What is a session and why is it important?

SMS is innately stateless. When a message from a cell phone arrives, it’s the Service Layer’s responsibility to identify which application to send this message to. The Service Layer maintains a table of sessions (virtual links with phone numbers and applications). If there’s a record for the cell phone number in question, it knows the application to send the message body to.

Once a user is in session with your application, you can treat a shared SMSC as though it were dedicated, with a wide-open keyword space. For instance, if you’re building a chat application, there’s no need for your users to memorize strange commands, like “*reply to every message with MYCHATKEYWORD then your message*,” in order to send in free-form messages. Just initiate a session and let them text naturally.

### How are sessions established?

If there’s no record in the sessions table, the Service Layer takes the body of the message and attempts to find an application that is expecting something resembling that message body. For example, if your application is associated with the keyword `Surf`, when a message with this body arrives, the Service Layer will establish a virtual link between the source phone number and your application. All of the following messages (no matter the content) from this phone number will be sent directly to your application until the session expires (based on
inactivity type) or until the phone number sends an opt-out message, such as `STOP`.

For applications using dedicated SMSCs with one or many DIDs, all messages sent to those DIDs are automatically routed to the application.

Keywords
--------

### What are keywords?

Traditionally (insofar as SMS has traditions), keywords were the primary means of interacting with a text messaging system. A user can text in a predefined keyword to begin interacting with an automated system, to be routed to a specific application or person.

With our API, keywords are used to identify which application a user intends to talk to. Any application can have many keyword associations. All keywords can be matched in either `Starts with` or `Matches exactly` modes. We treat keywords as only the starting point for a truly functional SMS application.

### Why do I need keywords?

You can have a completely open-ended application, on a dedicated SMSC, where all inbound messages arrive for you to parse. Or you can add structure, where users initiate conversations with your application by texting in a predefined keyword, so that you know what they intend to do and can then decide where to route them. On a shared SMSC, you'll need users to text into a keyword or initiate the conversation with an outbound message.

When a message arrives from a phone number with no active session, we scan it for keywords and see which application matches, create a session for it and send the message over.

### What are the `Starts with` and `Matches exactly` modes?

`Starts with` mode matches any keywords a user texts in that begins with the keyword you associate. For example, if you have a weather forecasting application, you may want to associate the keyword **Forecast** and set the mode to `Starts with`. That will allow your users to send messages like **Forecast Miami, Florida**. The Service Layer will see your target keyword at the beginning, establish a session and send the whole message to your application
for processing.

`Matches exactly` mode is used when the message is supposed to contain *only* the target keyword. It can have spaces and letters in mixed cases, but only this keyword will match and your application will be selected.

Note that keywords are case insensitive. Talk to us if you need more advanced tools, like RegEx-generated keywords.

### What are the `Auto-subscribe` and `Auto-subscribe Tags`?

If you have the Subscription Module enabled for your application, you can create keywords to automatically subscribe users. If you specify a list of tags, they will be used to tag the user when being subscribed through this keyword.

You can then send messages to groups of users by tags.

### What is `Don’t start session`?

Imagine that you have an app that just sends one-off responses, like weather forecasts for a given area or time table information for a particular station. You don’t need to maintain a persistent session between the user and the application.

Another scenario is when your application sends alerts of different types and you want to minimize the implementation effort. For different keywords, you enable the auto-subscription feature (along with the
Subscription Module) and auto-tag the users without creating a session.

Then, a user can send several keywords one after another and all you will need to do is to send messages to your subscribers filtered by tags.

### What is `Auto-response`?

The auto-response is an automatic reply sent to users in response to a specific keyword. It can be used with the other options in different combinations. In the above scenario, the auto-response can be used to send confirmations back to the users saying that you’ve successfully subscribed them to your alerts.

This feature has a side-effect. If you use the Subscription Module in your application and the Auto-response for the keyword that has auto-subscription enabled, your users will receive at least two messages - one for your Auto-response and another one for the confirmation on successful subscription.

We say at least two messages, because there is a possible third message. If enabled, this could be the *First-Timers Message* when the user texts your system the first time. That's entirely optional, but helpful if you're building a system with deeper interaction, where you'd like to provide an introductory instructional message. Or, generally, if you'd like all first-time users to receive a piece of information that's most relevant at the beginning, like your contact information separate from the subscription welcome message.

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
send messages to pre-defined groups, using our tagging
system.

### How do I put people on the subscribers list using the Subscription Module?

If you intend to use our Subscription Module features, for example, for
sending bulk messages, the only way to put a phone number on the list is
to let them subscribe themselves. You cannot tell the system to add
numbers to the list, as we keep our system compliant with the **Mobile
Marketing Association’s Best Practices** and other regulations.

Users must go through the full opt-in cycle and confirm that they indeed
want to be subscribed, preventing unsolicited messaging.

### Can I unsubscribe people from the Subscription Module?

Currently, no. Users can only unsubscribe themselves. However, we’ll
consider adding this feature if there’s enough interest.

### What are `tags`?

Tags are used to organize your subscribers in a free-form fashion,
familiar to users of Facebook, Flickr or any number of other web applications.

It’s possible to have a flat subscribers list, but you may want to split
it into groups so that you can address each one separately when sending
bulk messages. Tags can be stacked and tagged lists rearranged in an
intuitive, non-hierarchical way. We use these in place of *categories*
and *lists*.

Tags make it easy to do any kind of layered segmentation. Perhaps you'd like to divide your sports team into groups for defense, offense, or coaches. Or you can block out groups under different manager's purview, easily sending out group messages.

### How do I tag subscribers?

There are two simple ways to assign tags:

- If you use the Subscription Module, you
will receive a `subscription_created` callback every time someone
subscribes. In the response to this message, you can specify a
comma-separated list of tags for this particular number. The
Service Layer will receive the response and tag your new subscriber as
necessary.

- If you have some existing subscribers and want to tag them, you can
use the `tag_subscribers` API call with the desired tags and the phone
numbers to assign tags to existing numbers.

### How do I untag subscribers?

If at any point you need to remove tags from some numbers on your subscriber list, you can use the `untag_subscribers` API call.

Static responses
----------------

### What are Static responses used for?

Static responses let you build a basic SMS application without writing any code. If all you need is a canned
responses to a given set of keywords, you can enter them through your application ‘edit’ screen and the Service Layer will automatically send those back to your users when a matching message arrives.

For example, if you want to send your business card to everyone who texts **Jack** to your application, you could write an program that would receive a message from the Service Layer, see if it reads **Jack** and respond. But with Static responses, you can simply tell the Service Layer to send your desired text any time it sees an incoming message matching **Jack**.

### When do Static responses come into play -- or why doesn’t my Static Response work?

Static Responses are canned responses to known client messages. They work exactly as if the message was sent
to your application, recognized and replied with predefined text.

This means that in order for the Static Responses to work, there has to be a session established between the phone number and your application first. If there’s no session between the phone number and your application, we don’t know which application to send a message to, and thus it never reaches your Static Responses.

If you’d like to set up simple auto-responders when there’s no session in place, you can simply set up a keyword with an `auto-response`.

You can find details on how Sessions work in the [corresponding section](https://github.com/CarouselSMS/API/blob/master/sections/api/sessions.md).

Customizing module messages
---------------------------

There are three main modules that work together with an application -- the *Welcome*, *Help* and *Subscription* modules. Each of them has associated messages that can be customized or left blank, in which case nothing will be sent to the end user when triggered. We’ll examine them in the following sections.

### Welcome message

Every application can be configured to welcome its new users with a message. We know when it’s the first time someone has texted you and can send a reply to them automatically, but we also allow you to provide
your own content. Think of this welcome message as an optional additional message. You can leave it blank if you don’t need it.

### Help message

If your response to **HELP** message never changes, you may want to use our next module -- the **Help Module**. It will send an automatic response to anyone asking for help. If you leave this message blank, the help request
will be sent to your application as any other message, with no automatic reply sent to the user.

### Subscription messages

We have two types of messages that work only when the Subscription Module is enabled:

- **Subscribe message** -- used to confirm that the user has been subscribed successfully.
- **Stop message** -- used to confirm a successful unsubscribe.

Customize these messages to include a name and links to your web site.

&#8617; [Home](https://github.com/CarouselSMS/API)
--------------