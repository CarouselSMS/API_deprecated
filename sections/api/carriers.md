Carriers (*disabled for now*)
========

This set of calls lets the application work with carrier data.

Carrier Info `(carrier_info)`
-----------------------------

Query for carrier info for the given phone number.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` -- *string* -- phone number to get info for (10 digits in
    arbitrary format)

### Responses

-   `HTTP Code 500` and error message in the body
-   `HTTP Code 200` with JSON hash (text/javascript):
    -   `:id` -- internal carrier ID, unique for every carrier (e.g. 34,
        140, etc.)
    -   `:name` -- human-readable carrier name (e.g. Verizon, T-Mobile, etc.)

