Callbacks - subscriptions
=========================

Service Layer, when it takes care of the subscription management
(Subscription Module is enabled for the application), consumes all
messages related to the subscription cycle, such as STOP, SUB, Y and
others. In order to still let the application know and react to
subscription/cancellation events, we provide convenient callbacks.

Subscription Created `(subscription_created)`
---------------------------------------------

This callback is performed when a new subscription is created. The
application may decide that this particular subscription has to be
tagged in some way. If it does, the comma-separated list of tags can be
returned as the HTTP response to this callback request.

Tags can contain: **spaces, letters, digits, ’-’ and ‘\_’ characters**.

### Parameters:

- `type` -- `subscription_created`
- `phone_number` -- phone number of a new subscriber

### Responses:

-   Empty response if no tagging is required
-   Comma-separated list of tags to assign to the corresponding
    subscription record

Subscription Canceled `(subscription_canceled)`
-----------------------------------------------

This is invoked when a user decides to unsubscribe from the application.

### Parameters:

-   `type` -- `subscription_canceled`
-   `phone_number` -- phone number of the unsubscribed user
