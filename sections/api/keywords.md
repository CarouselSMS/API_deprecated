Keywords
========

This set of calls allows an application to associate/dissociate keywords with itself. All necessary checks are performed automatically to avoid conflicts.

Other types of API calls
------------------------

- #### [Sending messages](https://github.com/RecessMobile/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/RecessMobile/API/tree/master/sections/api/sessions.md)

- #### [Handling subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/subscriptions.md)


Validate keyword `(validate_keyword)`
-------------------------------------

Checks a keyword for validity and uniqueness.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `keyword` -- *string* -- keyword
-   `mode` -- *integer* -- `0` -- match exactly (default), `1` -- starts with

### Responses

-   `HTTP Code 200` with JSON hash (text/javascript):
    -   `errors` - optional array of keyword-related error messages. If
        this element isn’t present, the operation was successful.

Associate keyword `(associate_keyword)`
---------------------------------------

Associates the keyword with the application.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `keyword` -- *string* -- keyword
-   `mode` -- *integer* -- `0` -- match exactly, `1` -- starts with
-   `auto_subscribe` -- *boolean, optional* -- `TRUE` -- keyword will initiate
    the subscription
-   `auto_subscribe_tags` -- *string, optional* -- comma-separated list of
    tags to assign to the newly created auto-subscription

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200` with JSON hash (text/javascript):
    -   `errors` - optional array of error messages, in case of any
        problems with the keyword registration (duplicates, incorrect
        format, etc.). If this element isn’t present, the operation was
        successful.

Dissociate keyword `(dissociate_keyword)`
-----------------------------------------

Breaks the link between the keyword and the application.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `keyword` -- *string* -- keyword

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200` with JSON hash (text/javascript):
    -   `errors` - optional array of error messages. For example, if the
        keyword belongs to a different application.


&#8617; [Home](https://github.com/RecessMobile/API)
--------------