Callbacks - subscriptions
=========================

The Service Layer, when enabled to handle subscription management (the Subscription Module is toggled within the Service Layer UI), consumes all messages related to the subscription cycle, such as `STOP`, `SUB`, `Y` and others. 

For your application to know about and respond to subscription and cancellation events, we provide convenient callbacks.

Other callbacks sections
------------------------

- ### [General information and introduction to callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-general.md)

- ### [Sessions](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-sessions.md)

Subscription created `(subscription_created)`
---------------------------------------------

This callback is performed when a new subscription is created. Your application may decide that this particular subscription has to be tagged in some way. If it does, a comma-separated list of tags can be returned as the HTTP response to this callback request.

**Tags can contain**: *spaces*, *letters*, *digits*, '*-*' and '*\_*' *characters*.

### Parameters

- `type` -- `subscription_created`
- `phone_number` -- phone number of a new subscriber

### Responses

-   Empty response if no tagging is required
-   Comma-separated list of tags to assign to the corresponding subscription record

Subscription canceled `(subscription_canceled)`
-----------------------------------------------

This is invoked when a user decides to unsubscribe from the application.

### Parameters

-   `type` -- `subscription_canceled`
-   `phone_number` -- phone number of the unsubscribed user

&#8617; [Home](https://github.com/RecessMobile/API)
--------------
