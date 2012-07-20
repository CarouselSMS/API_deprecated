Callbacks - notifications
=========================

For your application to know about and respond to misc application events, we provide convenient callbacks.

Other callbacks sections
------------------------

- ### [General information and introduction to callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-general.md)

Phone blacklisted `(phone_blacklisted)`
---------------------------------------------

This callback is performed when a phone number was blacklisted. Usually that's a result of receiving special keyword by STOP module.

### STOP keywords

- STOP
- END
- QUIT 
- CANCEL 
- UNSUBSCRIBE 
- Q 
- STP 
- RE: STOP
- RE:STOP 
- REMOVE 
- TERMINATE 
- OPT OUT

### Parameters

- `phone_number` -- blacklisted phone number


Phone unblacklisted `(phone_unblacklisted)`
-----------------------------------------------

This is invoked when a phone number was unblacklisted by STOP module.

### OPT-IN keywords

- SUB
- SUBSCRIBE
- OPT-IN
- OPT IN
- START

### Parameters

-   `phone_number` -- unblacklisted phone number

Auto-reply loop detected `(auto_reply_loop)`
-----------------------------------------------

Sometimes application response and user auto-responder may organise infinite loop of messages. In such cases we inform you to take the necessary measures.

### Parameters

-   `phone_number` -- user phone number

&#8617; [Home](https://github.com/RecessMobile/API)
--------------