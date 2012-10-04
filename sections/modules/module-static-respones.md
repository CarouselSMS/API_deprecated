Module - static responses (**deprecated**)
=========================

The Static responses module provides a flexible feature: automated responses to certain keywords. These are available at the applications or SMSC levels.

Static responses are stored in the table where keywords are associated with responses. When an MO arrives, its contents are checked against the table associated with the target application (or with SMSC it came through if no application is currently associated with the phone number). If the message finds a response, the client application never receives it. Instead, an MT is sent automatically.

An application or SMSC can have any number of static responses. These can be registered through the application (or SMSC) configuration UI. Every message can have a Free flag set which means that the response has to be sent as an FTEU message. Note that FTEU is not available by default.

Other modules
-------------

- ### [General information and introduction](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-general.md)

- ### [Help module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-help.md)

- ### [Subscriptions](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-subscriptions.md)

- ### ["Welcome" module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-welcome.md)


Configuration
-------------

**Keyword-Response** pairs can be entered on the application/SMSC configuration UI.


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------