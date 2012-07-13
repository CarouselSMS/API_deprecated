Callbacks - general
===================

Client applications receive callbacks from the Service Layer through
their Gateway URL. There are difference callbacks that let the
application know of certain events with the user sessions, subscriptions
and more.

Format
------

Callback date and type are set as individual fields in the POST request
to the client application.

- Field `type` contains the name/type of the function
- Field `api_key` contains the API key of the app the callback belongs
to (in case several SL apps report to the same client-side app)
- Other fields contain additional information that may be useful to the
application in its processing of the callback -- phone numbers, message
bodies and other parameters.

Implementation on the Client Application side
---------------------------------------------

Callbacks aren’t required to be implemented. In fact, you can ignore all
of them, although this application may be not very useful. We imagine
that you will want to at least listen to incoming messages through the
`incoming_message` callback.

### Responses

Some of callbacks have optional responses expected, such as the list of
tags to assign to a newly created subscription . The format of the
response is currently set to the plain text, but later this may be
changed to the JSON. This step may be required to facilitate rich and
structured responses.

### Processing

It’s suggested that you process the callback as fast as possible on the
client application side to release Service Layer resources.

Incoming Message `(incoming_message)`
-------------------------------------

Received when new MO arrives and it’s routed to this client application.

When the message initiates the session and the keyword that was a match
is marked as for the auto-subscription, the `auto-subscribe` flag is set
meaning that after this callback is processed there will be an automatic
subscription of the texter performed by the service layer. As the result
of this process, there will be a subscription confirmation message sent
to the texter, meaning that you may decide not to send a normal response
from this call to avoid sending two messages.

If the message is marked as `auto_responded`, it means that the texter
has already received the message that was associated with the keyword.
You may choose to send another message or stay silent to avoid
duplicates.

### Parameters

- `type` -- `incoming_message`
- `phone_number` -- phone number of a texter
- `body` -- message body
- `sent_at` -- origination timestamp
- `auto_subscribe` -- *boolean, optional* -- flags that this message
initiated the session with auto-subscription
- `auto_responded` -- *boolean, optional* -- flags that this message was
already responded with the keyword-associated message
- `carrier_id` -- *optional* -- carrier ID
- `carrier_name` -- *optional* -- carrier name

### Responses

-   Empty response not to send anything back to the texter
-   The message to send
-   JSON-formatted string with any number of the following keys:
    -   `body` -- *string* -- the reply message body
    -   `close_session` -- *boolean* -- instruction to close the session
        between the phone number and this app, so that any following
        incoming messages are not be routed directly to this app
    -   `reprocess` -- *string* -- a text to send as an incoming message on
        behalf of the phone number that has sent the presently handled
        message. In combination with `close_session` it’s a powerful
        mechanism of transferring control to another application or
        redirecting to itself with a different keyword.

#### Example of JSON response

`{"body":"Switching to another app","close_session":true,"reprocess":"another keyword"}`

After receiving this response, the SL will:

1. Send a message "*Switching to another app*" as a response to the initial
MO.
2. Close the session between the app and the phone.
3. Pretend to receive (will send it to itself) an MO with text "*another
keyword*" from the same phone.

Delivery report `(delivery_report)`
-----------------------------------

When the message is sent with `send_message` (either in the future or
immediately), the list of message IDs is returned. Each ID represents
the part of the original message if it was larger than the maximum
allowed number of characters in the single SMS message.

### Parameters

-   `message_id` -- ID of the message the status of which has changed
-   `final` -- *boolean* -- `TRUE` if this report is final and no updates are to
    be expected
-   `status` - new status of the message, where possible values are:
    -   `0` -- Pending delivery
    -   `1` -- Delivered
    -   `2` -- Delivery failed
    -   `4` -- Queued for delivery

### Responses

-   `Ignored` -- This is a one-way fire and forget notification.
