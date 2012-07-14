Module - welcome
================

The welcome module is intended to send "Welcome" responses to first-time users of either SMSCs or applications.

Other modules
-------------

- ### [General information and introduction](https://github.com/RecessMobile/API/tree/master/sections/modules/module-general.md)

- ### [Help module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-help.md)

- ### [Static Responses](https://github.com/RecessMobile/API/tree/master/sections/modules/module-static-respones.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/modules/module-subscriptions.md)


How it works
------------

This module works on two levels: SMSCs and applications. In most cases, responses belong to a specific application and they will be pass through the application-level module. In rare cases, when a message is not associated with any application, the SMSC-level module will be used.

This module doesn’t stop processing of the message. It sends the welcome message (if filled out; no message is sent if left empty) in addition to the further processing which may or may not result in any additional messages.

Configuration
--------------

**Welcome text message** -- the message to send. If the message is not
    given, the module is inactive. The message field can be found on the
    application and SMSC edit page in the Service Layer UI.

&#8617; [Home](https://github.com/RecessMobile/API)
--------------