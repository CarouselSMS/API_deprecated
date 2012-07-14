Modules - general
=================

The Service Layer uses various modules to save you the trouble of developing common pieces SMS business logic.

Modules
-------

- ### [Help module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-help.md)

- ### [Static Responses](https://github.com/RecessMobile/API/tree/master/sections/modules/module-static-respones.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/modules/module-subscriptions.md)

- ### ["Welcome" module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-welcome.md)


Basics
------

Modules let developers to add more standard processing options to the Service Layer. Modules are called whenever an incoming message arrives to the application. The modules are expected to return either `nil` if they don’t
know how to handle the message, or a hash with the following fields:

-   `body` -- *string* -- the response message to return to the cell phone.
    - *empty* -- no response
-   `free` -- *string* -- `TRUE` to send the response through the FTEU
    gateway
    - This is used only in cases where FTEU messaging is available. Please contact us if interested.

Modules are organized in a chain, and are processed in sequence.

![Processing MO modules](https://github.com/RecessMobile/API/raw/master/images/Processing_MO__modules_.png)

If the first module returns a result, the second listed isn’t called nor instantiated.

One example of a module is in subscription processing. Given that many applications share this functionality, we extract the processing of keywords **SUB**, **Y**, **STOP** in a module and place it before the *Client
App Call* module. Then, if one of these keywords arrives, we can process them on the Service Layer instead of sending the request to your application.

An application can use any number of modules.


&#8617; [Home](https://github.com/RecessMobile/API)
--------------
