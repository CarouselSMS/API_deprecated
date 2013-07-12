Service Layer API documentation
============================
---

_DEPRECATED_
============

See [CarouselSMS.com/#documentation](http://carouselsms.com/#documentation) instead.


---


Endpoint
-----

    http://sl.carouselsms.com/api/

**Format of Request**: HTTP POST to endpoint with [URL encoded](http://en.wikipedia.org/wiki/Percent-encoding) parameters.

**Format of Response**: [JSON](http://json.org).

Examples:

    curl 'http://sl.carouselsms.com/api/send_message?api_key=API_KEY&body=test&phone_number=+1(347)264-3707'
    {"message_ids":"5554055"}
 
    curl 'http://sl.carouselsms.com/api/send_messages?api_key=API_KEY&template=Hello,%20%7B%7Bname%7D%7D&recipients=%7B%2213472643707%22:%7B%22name%22:%22Alex%22%7D,%221234567890%22:%7B%22name%22:%22Unknown%22%7D%7D' 
    {"message_ids":"5554173"}
    * without encoding URL looks like: http://sl.carouselsms.com/api/send_messages?api_key=API_KEY&template=Hello, {{name}}&recipients={"13472643707": {"name": "Alex"}, "1234567890": {"name": "Unknown"}}
    
API key
--------

Every client Application (app) has an API key associated with it. This
key is generated during the creation of the app and can be re-generated
from the show/edit screens in the administrative console.

This key uniquely identifies an app during the calls the app does to the
Service Layer (SL).

Methods
---

- #### [Dealing with keywords](https://github.com/CarouselSMS/API/tree/master/sections/api/keywords.md)

- #### [Sending messages](https://github.com/CarouselSMS/API/tree/master/sections/api/messaging.md)

- #### [Managing sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/sessions.md)

- #### [Blacklist](https://github.com/CarouselSMS/API/tree/master/sections/api/blacklist.md)

Data types
----------

Types of parameters being passed with API calls and received as callbacks:

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


Modules
-------

The SL uses a series of modules to provide basic business logic for applications.

- ### [General information and introduction](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-general.md)

- ### [Help module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-help.md)

- ### ["Welcome" module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-welcome.md)


Callbacks
---------

The following links provide detailed documentation on callbacks.

- ### [General information and introduction to callbacks](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-general.md)

- ### [Sessions](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-sessions.md)

- ### [Notification callbacks](https://github.com/CarouselSMS/API/tree/master/sections/api/callbacks-notifications.md)

Definitions
-----------

-  **Handset**, **Phone**: an end-user's mobile phone.
-  **MT** (**M**obile **T**erminated): outgoing message from our system to a handset.
-  **MO** (**M**obile **O**riginated): incoming message from a handset to our system.
-  **DID** ([**D**irect **I**nward **D**ialing](http://en.wikipedia.org/wiki/Direct_inward_dialing)): the term we use for virtual numbers or long codes. These are 10-digit phone numbers in the United States.
-  **SMSC** ([**S**hort **M**essage **S**ervice **C**enter](http://en.wikipedia.org/wiki/Short_message_service_center)): the point in the stack which stores and delivers text messages. In our case, we use internal SMSCs which can be made up of one DID or many. Multiple DIDs allow for threaded conversations and higher throughput.

[FAQ](https://github.com/CarouselSMS/API/tree/master/FAQ.md)
----



License
=======

The Carousel API documents are Copyright © 2013 [Recess Mobile](http://recess.im/).
