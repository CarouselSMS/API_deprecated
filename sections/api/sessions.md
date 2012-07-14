Sessions
========

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/RecessMobile/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/RecessMobile/API/tree/master/sections/api/messaging.md)

- #### [Handling subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/subscriptions.md)


Close sessions `(close_sessions)`
---------------------------------

Closes active sessions between the application and phone numbers.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_numbers` -- *string* -- comma-separated list of phone numbers (10
    digits with or without country code) to close the session with.

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200`


&#8617; [Home](https://github.com/RecessMobile/API)
--------------