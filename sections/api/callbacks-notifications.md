Callbacks - notifications
=========================

For your application to know about and respond to misc application events, we provide convenient callbacks.

Other callbacks sections
------------------------

- ### [General information and introduction to callbacks](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-general.md)

- ### [Sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-sessions.md)

- ### [Subscription-related callbacks](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-subscriptions.md)

Phone blacklisted `(phone_blacklisted)`
---------------------------------------

This callback is performed when a phone number is blacklisted. Usually that's the result of receiving one of special opt-out keywords addressed by the *STOP module*.

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
- A series of related natural language variations

### Parameters

- `phone_number` -- the blacklisted phone number


Phone unblacklisted `(phone_unblacklisted)`
-------------------------------------------

This is invoked when a phone number is unblacklisted by the *STOP module*.

### OPT-IN keywords

- SUB
- SUBSCRIBE
- OPT-IN
- OPT IN
- START

### Parameters

-  `phone_number` -- unblacklisted phone number

Auto-reply loop detected `(auto_reply_loop)`
--------------------------------------------

Sometimes, an application response and user auto-responder may unintentionally initiate an infinite loop of messages. Let's say you send `Hello` to user `Foo`'s phone, which is set a vacation auto-response (or anything else clever, but not clever enough). Your application, to be helpful, replies with `Sorry, we don't know what you mean!`, which returns `Foo`'s vacation response once more. Or worse, `Foo`, isn't a proper phone at all, but another application with no rate limit.

In such cases, we inform you in order for your application to take the necessary measures.

### Parameters

-   `phone_number` -- user phone number

&#8617; [Home](https://github.com/CarouselSMS/API)
--------------