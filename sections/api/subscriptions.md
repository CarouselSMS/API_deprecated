Subscriptions (**deprecated**)
=============

Calls for managing subscribers and sending them messages.

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/CarouselSMS/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/CarouselSMS/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/sessions.md)


Tag subscribers `(tag_subscribers)`
-----------------------------------

Assigns a list of tags to a series of phone numbers belonging to your subscribers.

### Parameters

-   `api_key` -- *string* -- API key of the application.
-   `tags` -- *string* -- comma-separated list of tags.
-   `phone_numbers` -- *string* -- comma-separated list of phone numbers with
    or without the country code.

### Responses

-   `HTTP Code 500` and error message in the body.
-   `HTTP Code 200`

Un-tag subscribers `(untag_subscribers)`
----------------------------------------

Removes listed tags from phone numbers (all or specific ones, if they are given).

### Parameters

-   `api_key` -- *string* -- API key of the application.
-   `tags` -- *string* -- comma-separated list of tags.
-   `phone_numbers` -- *string, optional* -- comma-separated list of phone
    numbers with or without the country code.

### Responses

-   `HTTP Code 500` and error message in the body.
-   `HTTP Code 200`

Count tagged subscribers `(count_tagged_subscribers)`
-----------------------------------------------------

Returns the number of subscribers in each tag.

### Parameters

-   `api_key` -- *string* -- API key of the application.
-   `tags` -- *string* -- comma-separated list of tags.

### Responses

-   `HTTP Code 500` and error message in the body.
-   `HTTP Code 200` with JSON hash (text/javascript), mapping tag-count pairs.

Send subscription message `(send_subscription_message)`
-------------------------------------------------------

Sends a message to the application's subscribers. The message is automatically split into multiple parts using the preferred application splitting mode.

If a list of tags is given, subscribers with those tags are selected. If no tag is specified, all subscribers receive the message.

If a time in the `on` field is given, the call schedules a message for future delivery.

The message text will be split and otherwise processed in the same way as a regular subscription message.

The scheduled date of message delivery must be set for the next day or later. The date can contain a
suggested time. The application will use it for guidance. The message is guaranteed to not be sent before this time, but can be sent later. The messages are scheduled to be sent in batches periodically during the day (currently every two hours). The format of the date may vary from the strict `10/12/2008 12:55AM -0500` to the relaxed `Tuesday 9 1:15PM`. If the timezone isn't specified, then `EST` is assumed.

### Parameters

- `api_key` -- *string* -- mandatory API Key.
- `body` -- *string* -- message text.
- `on` -- *string, optional* -- time when the message is to be sent.
- `tags` -- *string, optional* -- comma-separated list of tags.
- `description` -- *string, optional* -- description of this message or any other info that you may want to save.

### Responses

- `HTTP Code 500` and error message in the body.
- `HTTP Code 200` with JSON hash (text/javascript).
	- If it's an immediate subscription message:
		- `recipient_count` -- number of recipients that received the message.


Cancel subscription messages `(cancel_subscription_messages)`
-------------------------------------------------------------

This call cancels subscription messages scheduled for future delivery (those messages which use the `send_subscription_message` call with the parameter `on`). The `send_subscription_message` call returns the list of IDs corresponding to all scheduled messages. You can use these IDs to cancel future messages at any time.

Please note that this call is for scheduled **subscription** messages.
Use the [`cancel_messages` call](https://github.com/CarouselSMS/API/blob/master/sections/api/messaging.md) for cancellation of regular (non-subscription) scheduled messages.

### Parameters

-   `message_ids` -- *string* -- comma-separated list of scheduled subscription message IDs

### Responses

-   `HTTP Code 500` and error message in the body.
-   `HTTP Code 200`
    -   `canceled_count` -- *integer* -- the number of canceled messages.


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------