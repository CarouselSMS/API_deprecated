Service Layer API documentation
===============================

API documentation for Service Layer (**SL**) API.

Sign up for an invitation ahead of our public launch, at [carouselsms.com](http://carouselsms.com).


API keys
--------

Every client Application (app) has an API key associated with it. This
key is generated during the creation of the app and can be re-generated
from the show/edit screens in the administrative console.

This key uniquely identifies an app during the calls the app does to the
SL.

Modules
-------

The SL uses a series of modules to provide basic business logic for applications.

- ### [General information and introduction](https://github.com/RecessMobile/API/tree/master/sections/modules/module-general.md)

- ### [Help module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-help.md)

- ### [Static Responses](https://github.com/RecessMobile/API/tree/master/sections/modules/module-static-respones.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/modules/module-subscriptions.md)

- ### ["Welcome" module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-welcome.md)


Callbacks
---------

The following links provide detailed documentation on callbacks.

- ### [General information and introduction to callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-general.md)

- ### [Sessions](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-sessions.md)

- ### [Subscription-related callbacks](https://github.com/RecessMobile/API/tree/master/sections/api/callbacks-subscriptions.md)


Calls
-----

All calls should be performed with POST request. The API Key (`api_key`)
is the only form field required to be present in every call to the
SL.

There’s an API URL that is used at all times to which the name of the
operation is appended:

### URL
`http://sl.recessmobile.com/api/<operation>` or
`https://sl.recessmobile.com/api/<operation>` (SSL support)

### Types of calls

- #### [Dealing with keywords](https://github.com/RecessMobile/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/RecessMobile/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/RecessMobile/API/tree/master/sections/api/sessions.md)

- #### [Handling subscriptions](https://github.com/RecessMobile/API/tree/master/sections/api/subscriptions.md)


Data types
----------

Parameters that you specify in calls to the API and receive as callbacks
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
parsing almost everything that can be interpreted as a date/time.
Here are some examples of what the dates can look like:

-   `16:30` – takes current date as basis and uses provided time
-   `Aug 31` – take current year, users the given date and sets time
    to 00:00
-   `7/31` – the same as above
-   `2/9/2007` or `2007-02-09` – date only
-   `02-09-2007 12:30:44 AM` or `2007-09-02T00:30:44Z` - *UTC (GMT)*
    time
-   `02-09-2007 12:30:44 PM EST` or `2007-09-02T12:30:44-0500` -
    localized time
-   `Wednesday, January 10, 2001` - human-readable date

If you need a stricter definition, you can refer to [RFC2822 (3.3. Date
and Time Specification)](http://www.faqs.org/rfcs/rfc2822.html).

Definitions
-----------

-  **Handset**, **Phone**: an end-user's mobile phone.
-  **MT** (**M**obile **T**erminated): outgoing message from our system to a handset.
-  **MO** (**M**obile **O**riginated): incoming message from a handset to our system.
-  **DID** ([**D**irect **I**nward **D**ialing](http://en.wikipedia.org/wiki/Direct_inward_dialing)): the term we use for virtual numbers or long codes. These are 10-digit phone numbers in the United States.
-  **SMSC** ([**S**hort **M**essage **S**ervice **C**enter](http://en.wikipedia.org/wiki/Short_message_service_center)): the point in the stack which stores and delivers text messages. In our case, we use internal SMSCs which can be made up of one DID or many. Multiple DIDs allow for threaded conversations and higher throughput.

[FAQ](https://github.com/RecessMobile/API/tree/master/sections/api/faq-general.md)
----

