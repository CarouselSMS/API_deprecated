Callbacks - sessions
====================

These are callbacks received around sessions.
The [FAQ](https://github.com/RecessMobile/API/tree/master/FAQ.md) has more details on the concept of sessions.

Other callbacks sections
------------------------

- ### [General information and introduction to callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-general.md)

- ### [Subscription-related callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-subscriptions.md)

Session closed `(session_closed)`
---------------------------------

This callback is performed when a user session with an application is closed for any reason. It can be the result of a session expiration or due to an explicit command from a user.

### Parameters

-   `type` -- `session_closed`
-   `phone_numbers` -- comma-separated list of user phone numbers


&#8617; [Home](https://github.com/RecessMobile/API)
--------------