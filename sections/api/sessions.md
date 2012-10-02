Sessions
========

Sessions are used to maintain connections between a user's phone and the application. See the [FAQ](https://github.com/CarouselSMS/API/tree/master/FAQ.md) for more.

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/CarouselSMS/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/CarouselSMS/API/tree/master/sections/api/messaging.md)

- #### [Blacklisting](https://github.com/CarouselSMS/API/tree/master/sections/api/blacklist.md)


Close sessions `(close_sessions)`
---------------------------------

Closes active sessions between the application and phone numbers.

### Parameters

-   `api_key` -- *string* -- API key of the application.
-   `phone_numbers` -- *string* -- comma-separated list of phone numbers (10
    digits with or without country code) with which to close the session.

### Responses

-   `HTTP Code 500` and error message in the body.
-   `HTTP Code 200`


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------