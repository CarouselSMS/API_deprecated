Subscriptions
=============

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/RecessMobile/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/RecessMobile/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/RecessMobile/API/tree/master/sections/api/sessions.md)


Tag subscribers `(tag_subscribers)`
-----------------------------------

Assigns the list of tags to the list of phone numbers among the
subscribers of your application.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `tags` -- *string* -- comma-separated list of tags
-   `phone_numbers` -- *string* -- comma-separated list of phone numbers with
    or without the country code

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`

Un-tag subscribers `(untag_subscribers)`
----------------------------------------

Removes the tags in the list from the phone numbers (all or specific, if
they are given).

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `tags` -- *string* -- comma-separated list of tags
-   `phone_numbers` -- *string, optional* -- comma-separated list of phone
    numbers with or without the country code

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`

Count tagged subscribers `(count_tagged_subscribers)`
-----------------------------------------------------

Returns the number of subscribers in each tag.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `tags` -- *string* -- comma-separated list of tags

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200` with JSON hash (text/javascript) with tag-count pairs

Send subscription message `(send_subscription_message)`
-------------------------------------------------------

Sends a message to the application subscribers. The message is split
into multiple parts using the preferred application splitting mode
automatically.

If the list of tags is given, subscribers with these tags are chosen. If
no tag is specified, all subscribers receive the message.

If the time in the `on` field is given the call operates in the
scheduling mode. It schedules a message to be sent to the application
subscribers in a future. The message text will be split and otherwise
processed as in the usual subscription message sending. The date of the
message sending has to be tomorrow or later. The date can contain the
suggested time and the application will use it as a guidance. The
message is guaranteed to not be sent before this time, but can be sent
later. The messages are supposed to be sent in batches periodically
during the day (currently every two hours). The format of the date may
vary from very strict `10/12/2008 12:55AM -0500` to the relaxed
`Tuesday 9 1:15PM`. If the timezone isn’t specified, then `EST` is assumed.

### Parameters

- `api_key` -- *string* -- mandatory API Key.
- `body` -- *string* -- message text.
- `on` -- *string, optional* -- time when the message is to be sent.
- `tags` -- *string, optional* -- comma-separated list of tags.
- `description` -- *string, optional* -- description of this message or any
other info that you want to save.

### Responses

- `HTTP Code 500` and error message in the body
- `HTTP Code 200` with JSON hash (text/javascript)
	- If immediate subscription message:
		- `recipient_count` -- number of recipients that received the message


Cancel subscription messages
----------------------------

This call cancels subscription messages scheduled for future delivery
with the `send_subscription_message` call with the parameter `on`. The
`send_subscription_message` call returned the list of IDs corresponding
to all scheduled messages. You can use these IDs to cancel future
messages at any moment.

Please note that this call is for scheduled **subscription** messages.
Use the `cancel_messages` call for regular future messages cancellation.

### Parameters

-   `message_ids` -- *string* -- comma-separated list of scheduled
    subscription message IDs

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`
    -   `canceled_count` -- *integer* -- the number of canceled messages


&#8617; [Home](https://github.com/RecessMobile/API)
--------------