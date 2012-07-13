Messaging
=========

Send Message `(send_message)`
-----------------------------

If an application needs to send a message to a certain phone number, it uses this call. The message can be of arbitrary size. If it doesn’t fit into the standard message size (160 characters), the message will be broken into several parts automatically, like this:

-   `(1/3) The beginning…`
-   `(2/3) …continuation …`
-   `(3/3) …the final piece.`

Scheduled messages are sent in batches every 15 minutes. The format of
the date (`on` field) may vary from very strict `10/12/2008 12:55AM —
0500` to the relaxed `Tuesday 9 1:15PM`. If the timezone isn’t
specified, then `EST (GMT-5)` is assumed.

### Split Modes

When message breaking is necessary, it can be performed in one of three
predefined ways. The way can be chosen on per-application basis and is
set in the Application preferences on the Service Layer side.

-   **Character Boundary** - the message will be split in part without
    looking for gaps between the words and the ends of sentences. It’s
    the most compact way of breaking the messages that ensures the
    minimal number of parts being sent.

-   **Word Boundary** - the message text is analyzed for the gaps between
    the words and split so that no word is broken unless the message
    becomes severely under-filled (more than a half of the message is
    empty). In this case the Character Boundary mode is used to fill the
    rest of the part and the operation switches back to normal Word
    Boundary operation for the next part.

-   **Sentence Boundary** - the message is broken into parts preferably on
    the sentence edges which are (commas, exclamation and question
    marks, and line breaks). Again if the message appears to be
    under-filled, the mode is switched to the Word Boundary and if even
    this doesn’t help, it is lowered to the Character Boundary.

### Test Number

Phone numbers which start with `555` are used for testing purposes.
Messages to these numbers will not be sent to a real phone number.

There's no charge for sending message to these numbers, which
can be used for testing.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- destination phone number
    (10 digits with or without country code) or a comma-separated list
    of phone numbers.
-   `body` -- *string* -- message text
-   `action_expected` -- *boolean, optional* -- send `TRUE` if a response
    from the target phone is expected. In this case, the session between
    the phone and the Application is established for seamless direction
    of the response MOs to the application without the need of sending
    the Keyword to select the Application first.
-   `on` -- *string, optional* -- time when the message is to be sent
-   `tag` -- *string, optional* -- conversation thread identifier. Messages
    with the same tag will be sent via one DID.

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`
    -   Comma-separated list of scheduled message IDs is returned with
        `message_ids` key. This is useful for matching sent
        messages with delivery reports and message cancellation.
        Negative IDs are possible in these cases:
    	-   `-1` -- if phone number was invalid
        -   `-2` -- if phone number is currently blacklisted
        -   `-3` -- if phone is being flooded reached the limit of
            messages for a configured period of time for this app

Send Messages `(send_messages)`
-------------------------------

Sometimes you need to send several slightly different messages to
several phone numbers. You could issue multiple 'send_message'
requests, but there’s a better way. You can specify a template to
use as the basis for your messages and then, for each number, you need only provide the different parts to paste into the template for each number. Here’s an example:

-   `template = "Hello {{name}}. You have {{credits}} credits remaining."`
-   `recipients = '{"0123456789": {"name": "John", "credits": "5"},
    "9876543210": {"name": "Mary", "credits": "10"}}'`

The phone number `0123456789` wil receive `Hello John. You have 5 credits
remaining.`, while the phone number `9876543210` will receive `Hello Mary. You have 10 credits remaining.`

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `template` -- *string* -- template string to use for generation of
    recipient messages.
-   `recipients` -- *string* -- JSON-hash with phone numbers (10 digits) as
    keys and the substitution hash as values. Each substitution hash
    contains the names of tags you mentioned in the template body as
    keys and the replacement values as values.
-   `action_expected` -- *boolean, optional* -- send TRUE if the response
    from the target phone is expected. In this case, the session between
    the phone and the Application is established for seamless directing
    of the response MOs to the application without the need of sending
    the Keyword to select the Application first.
-   `on` -- *string, optional* -- time when the message is to be sent.
-   `tag` -- *string, optional* -- conversation thread identifier. Messages
    with the same tag will be sent via one DID.

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`
    -   Comma-separated list of scheduled message IDs (in no particular
        order) is returned with the `message_ids` key. Negative IDs are
        possible in these cases:
        -   `-1` -- if phone number was invalid
        -   `-2` -- if phone number is currently blacklisted


Cancel Messages `(cancel_messages)`
-----------------------------------

This call cancels messages scheduled for future delivery with the
`send_message` call with parameter `on`. The `send_message` call returned
the list of IDs corresponding to all scheduled messages or parts of the
bigger message that didn’t fit into a single text message. You can use
these IDs to cancel future messages at any moment.

Please note that this call can cancel only non-subscription messages. To
cancel subscription-level messages, use the `cancel_subscription_messages`
call.

### Parameters

-   `message_ids` -- *string* -- comma-separated list of scheduled message
    IDs

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`
    -   `canceled_count` -- *integer* -- the number of canceled messages

Delivery status `(delivery_status)`
-----------------------------------

This call accepts a single sent message ID or the list of IDs separated
by commas and returns the status for each of the messages. If the
message wasn’t found, it’s not mentioned in the results. The statuses
have numeric values and are as follows:

-   `0` -- Pending delivery
-   `1` -- Delivered to the user phone
-   `2` -- Not delivered to the user phone (failed)

### Parameters

-   `message_ids` -- *string* -- comma-separated list of message IDs (either scheduled or not) returned from the `send_message` call

### Responses

-   The JSON-formatted map of found message IDs to their statuses

Remove Tag `(remove_tag)`
-------------------------

Allows to reuse conversation thread (application number) for
communication with other recipient using the same tag, frees application
number for new uses.

### Parameters

- `api_key` -- *string* -- API key of the application
- `phone_number` -- *string* -- phone number of message recipient.
- `tag` -- *string* -- conversation thread identifier.

### Responses

- `HTTP Code 500` and error message in the body
- `HTTP Code 200`


&#8617; [Home](https://github.com/RecessMobile/API)
--------------