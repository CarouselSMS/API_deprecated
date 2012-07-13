Service Layer API documentation
===============================

API documentation for Service Layer (**SL**) API.


API keys
--------

Every client Application (app) has an API key associated with it. This
key is generated during the creation of the app and can be re-generated
from the show/edit screens in the Service Layer (SL) administrative
console.

This key uniquely identifies an app during the calls the app does to the
SL.

Modules
-------

- ### [General](https://github.com/RecessMobile/API/tree/master/sections/api/module-general.md)

- ### [Help](https://github.com/RecessMobile/API/tree/master/sections/api/module-help.md)

- ### [Static Responses](https://github.com/RecessMobile/API/tree/master/sections/api/module-static-respones.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/module-subscriptions.md)

- ### [Welcome](https://github.com/RecessMobile/API/tree/master/sections/api/module-welcome.md)


Callbacks
---------

The following links provide detailed documentation on callbacks.

- ### [General](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-general.md)

- ### [Sessions](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-sessions.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-subscriptions.md)


Calls
-----

All calls should be performed with POST request. The API Key (`api_key`)
is the only form field required to be present in every call to the
service layer since it is necessary to identify the application.

There’s an API URL that is used at all times to which the name of the
operation is appended:

### URL
`http://sl.holmesmobile.com/api/<operation>` or
`https://sl.holmesmobile.com/api/<operation>` (SSL support)

### Types of calls

- #### [Keywords](https://github.com/RecessMobile/API/tree/master/sections/api/keywords.md)

- #### [Messaging](https://github.com/RecessMobile/API/tree/master/sections/api/messaging.md)

- #### [Sessions](https://github.com/RecessMobile/API/tree/master/sections/api/sessions.md)

- #### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/subscriptions.md)


Data types
----------

Parameters that you specify in the calls to API and receive in callbacks
from the API can be of different types.

### String

Regular text string.

### Integer

Integer number, either positive or negative.

### Boolean

We are quite flexible with booleans. They are case-insensitive and can take the following shapes:

-   `TRUE: 1, t, true, y, yes`
-   `FALSE: 0, f, false, n, no`

### Dates and times

Dates and times parsing is very liberal in the SL. We are capable of
parsing almost everything that can be interpreted as a date / time or
even a clue of them. Here are some examples of what the dates can look
like:

-   `16:30` – takes current date as basis and uses provided time
-   `Aug 31` – take current year, users the given date and sets time
    to 00:00
-   `7/31` – the same as above
-   `2/9/2007` or `2007-02-09` – date only
-   `02-09-2007 12:30:44 AM` or `2007-09-02T00:30:44Z` - UTC (GMT)
    time
-   `02-09-2007 12:30:44 PM EST` or `2007-09-02T12:30:44-0500` -
    localized time
-   `Wednesday, January 10, 2001` - human-readable date

If you need a stricter definition, you can refer to [RFC2822 (3.3. Date
and Time Specification)](http://www.faqs.org/rfcs/rfc2822.html).

Definitions
-----------

MO, MT, SMSC, DID coming...

[FAQ](https://github.com/RecessMobile/API/tree/master/sections/api/faq-general.md)
----

