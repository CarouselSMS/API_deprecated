Blacklist
========

This set of calls lets the application work with phone blacklisting.

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/CarouselSMS/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/CarouselSMS/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/sessions.md)


Blacklisting `(blacklist)`
-----------------------------

Adds phone numbers to blacklist.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- phone number
    (10 digits with or without country code) or a comma-separated list
    of phone numbers.

### Responses

-   A JSON-formatted map of specified phone numbers to statuses of blacklisting:
	- true -- phone number was successfully blacklisted;
	- false -- blacklisting operation failed.

Unblacklisting `(unblacklist)`
-----------------------------

Removes phone numbers from blacklist.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- phone number
    (10 digits with or without country code) or a comma-separated list
    of phone numbers.

### Responses

-   A JSON-formatted map of specified phone numbers to statuses of unblacklisting:
	- true -- phone number was successfully removed from blacklist;
	- false -- unblacklisting operation failed.	

Blacklisting status `(blacklist_status)`
-----------------------------

Query for blacklist status for the given phone numbers.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- phone number
    (10 digits with or without country code) or a comma-separated list
    of phone numbers.

### Responses

-   A JSON-formatted map of specified phone numbers to their blacklisting statuses:
	- true -- phone number is blacklisted;
	- false -- phone number is not blacklisted.	


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------