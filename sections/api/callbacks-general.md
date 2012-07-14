Callbacks - general
===================

Client applications receive callbacks from the Service Layer through their Gateway URL. There are different callbacks which notify applications about certain events involving user sessions, subscriptions, and more.

Other callbacks sections
------------------------

- ### [Sessions](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-sessions.md)

- ### [Subscription-related callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-subscriptions.md)

Format
------

Callback date and type are set as individual fields in the `POST` request to the client application.

- Field `type` contains the name/type of the function
- Field `api_key` contains the API key of the app to which the callback belongs
 (in case several SL apps report to the same client-side app)
- Other fields contain additional information that may be useful to the
application in its processing of the callback -- phone numbers, message
bodies and other parameters.

Implementation on the client application side
---------------------------------------------

You're not required to take advantage of callbacks. In fact, you can ignore all of them, although this application may be not very useful. You ought to at least listen for incoming messages through the `incoming_message` callback.

### Responses

Some of callbacks have optional responses expected, such as a list of tags to assign to a newly created subscription. The format of the response is currently set to the plain text, but later this may be changed to the JSON. This step may be required to facilitate rich and structured responses.

### Processing

We suggest that you process the callback as fast as possible on the client application side to release Service Layer resources.

Incoming message `(incoming_message)`
-------------------------------------

Received when a new MO arrives and is routed to your application.

When a message initiates a session and the matching keyword has auto-subscription enabled, the `auto-subscribe` flag is set. This means that after this callback is processed, the message sender is automatically subscribed on the Service Layer side. There will be a subscription confirmation message sent to the user, as configured in the Service Layer UI. You may decide not to send your own automated response from this call to avoid sending two messages.

If the message is marked as `auto_responded`, it means that the message sender has already received the automated response message that was associated with the keyword. You may choose to send another message or stay silent to avoid duplicates.

### Parameters

- `type` -- `incoming_message`
- `phone_number` -- phone number of a texter
- `body` -- message body
- `sent_at` -- origination timestamp
- `auto_subscribe` -- *boolean, optional* -- flags this message as
initiating a session with auto-subscription
- `auto_responded` -- *boolean, optional* -- flags that this message as having
already been responded to with the keyword-associated content
- `carrier_id` -- *optional* -- carrier ID
- `carrier_name` -- *optional* -- carrier name

### Responses

-   Empty response not to send anything back to the texter
-   The message to send
-   JSON-formatted string with any number of the following keys:
    -   `body` -- *string* -- the reply message body
    -   `close_session` -- *boolean* -- instruction to close the session
        between the phone number and this app, so that any following
        incoming messages are not be routed directly to this app.
        Note that dedicated SMSCs will still messages routed to the app, but out of session.
    -   `reprocess` -- *string* -- a text to send as an incoming message on
        behalf of the phone number that has sent the presently handled
        message. In combination with `close_session` it’s a powerful
        mechanism for transferring control to another application or
        redirecting to itself with a different keyword.

#### Example of JSON response

`{"body":"Switching to another app","close_session":true,"reprocess":"another keyword"}`

After receiving this response, the SL will:

1. Send a message "*Switching to another app*" as a response to the initial MO.
2. Close the session between the app and the phone.
3. Pretend to receive (will send it to itself) an MO with text "*another
keyword*" from the same phone.

Delivery report `(delivery_report)`
-----------------------------------

When the message is sent with `send_message` (either in the future or immediately), a list of message IDs is returned. If a message was longer than the maximum number of allowed characters and as a result was split into parts, each ID represents each of those parts.

### Parameters

-   `message_id` -- ID of the message the status of which has changed
-   `final` -- *boolean* -- `TRUE` if this report is final and no updates are to be expected
-   `status` - new status of the message, where the possible values are:
    -   `0` -- *Pending delivery*
    -   `1` -- *Delivered*
    -   `2` -- *Delivery failed*
    -   `4` -- *Queued for delivery*

### Responses

-   `Ignored` -- This is a one-way fire and forget notification.


&#8617; [Home](https://github.com/RecessMobile/API)
--------------