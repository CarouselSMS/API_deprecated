Service Layer API documentation
===============================

API documentation for Service Layer API.


Where do I start?
-----------------

Want to get started with API integration? Here's a quick check list:

1. [Register your app](http://integrate.37signals.com/apps/new) or [update your already registered app](http://integrate.37signals.com/) to access more products.
2. Review the [brand guidelines](#brand-guidelines) for rules on naming and marketing your app
3. Read up on how to [authenticate your app](#authentication) with our products.
4. Peruse the [API docs](#products) for the product you need to work with
5. Join the [API mailing list](http://groups.google.com/group/37signals-api) to talk to others using the APIs and give us feedback!


API Documentation
-----------------

Need to look up the API documentation for a product? There's a repo for each:

* [Basecamp API](https://github.com/37signals/bcx-api)
* [Basecamp Classic API](https://github.com/37signals/basecamp-classic-api)
* [Highrise API](https://github.com/37signals/highrise-api)
* [Campfire API](https://github.com/37signals/campfire-api)
* [Backpack API](https://github.com/37signals/backpack-api)
* [System Status API](http://status.37signals.com/api)


API Keys
--------

Every client Application (APP) has an API Key associated with it. This
key is generated during the creation of the APP and can be re-generated
from the show / edit screens in the Service Layer (SL) administrative
console.

This key uniquely identifies an APP during the calls the APP does to the
SL.

Definitions
-----------

MO, MT, SMSC, DID

Calls
-----

All calls should be performed with POST request. The API Key (`api_key`)
is the only form field required to be present in every call to the
service layer since it is necessary to identify the application.

There’s an API URL that is used at all times to which the name of the
operation is appended:

### URL:
<code>http://sl.holmesmobile.com/api/\<operation></code> or
<code>https://sl.holmesmobile.com/api/\<operation></code> (SSL support)

Data Types
----------

Parameters that you specify in the calls to API and receive in callbacks
from the API can be of different types.

### String

Regular text string.

### Integer

Integer number, either positive or negative.

### Boolean

We are quite flexible with booleans.

-   They are case-insensitive and can take the following shapes:
    -   `TRUE: 1, t, true, y, yes`
    -   `FALSE: 0, f, false, n, no`

### Dates and Times

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


