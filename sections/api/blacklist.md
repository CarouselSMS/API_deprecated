Blacklisting
============

This set of calls manages end-user blacklisting.

Users who opt-out are blacklisted, preventing them from receiving further messages.

You can unblacklist using these API calls, or by having the user text in a subscription keyword.

Other types of API calls
------------------------

- #### [Dealing with keywords](https://github.com/CarouselSMS/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/CarouselSMS/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/sessions.md)


Blacklisting `(blacklist)`
--------------------------

Adds phone numbers to the blacklist arbitrarily.

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

Removes phone numbers from the blacklist.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- phone number
    (10 digits with or without a country code) or a comma-separated list
    of phone numbers.

### Responses

-   A JSON-formatted map of specified phone numbers to their blacklist status:
  - true -- phone number was successfully removed from the blacklist
	- false -- unblacklisting operation failed	

Blacklisting status `(blacklist_status)`
----------------------------------------

Query for the blacklist status of a given phone number or numbers.

### Parameters

-   `api_key` -- *string* -- API key of the application
-   `phone_number` or `phone_numbers` -- *string* -- phone number
    (10 digits with or without a country code) or a comma-separated list
    of phone numbers.

### Responses

-   A JSON-formatted map of the specified phone numbers to their blacklist status:
  - true -- phone number is blacklisted
	- false -- phone number is not blacklisted


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------