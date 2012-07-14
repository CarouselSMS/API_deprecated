Modules - general
=================

Modules
-------

- ### [Help module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-help.md)

- ### [Static Responses](https://github.com/RecessMobile/API/tree/master/sections/modules/module-static-respones.md)

- ### [Subscriptions](https://github.com/RecessMobile/API/tree/master/sections/modules/module-subscriptions.md)

- ### ["Welcome" module](https://github.com/RecessMobile/API/tree/master/sections/modules/module-welcome.md)


Basics
------

Modules let developers to add more standard processing options to the
service layer. Modules are called when an incoming message arrives to
the application, and are expected to return either `nil` (if they don’t
know how to handle the message), or the hash with the following fields:

-   `body` -- *string* -- the response message to return to the cell phone
    (empty - no response)
-   `free` -- *string* -- `TRUE` to send the response through the FTEU
    gateway (this is used only in cases where FTEU messaging is available; please contact us if interested)

Modules are organized in the chain, and are processed
in this order. If the first module returns the result, the second listed
isn’t called and even not instantiated.

![Processing MO modules](https://github.com/RecessMobile/API/raw/master/images/Processing_MO__modules_.png)

The example of a module is the subscription processing. Given that many
applications share this functionality, we extract the processing of
keywords **SUB**, **Y**, **STOP** in a module and place it before the *Client
App Call* module so that if one of these keywords arrive, we can process
them ourselves on the Service Layer instead of sending the request to
the client application.

You can have any number of modules.

Configuration
-------------

Sometimes modules will require different configuration from application
to application. It’s suggested to have a separate table for
configuration options for a specific module and link it to the
application table through the 1-to-1 relationship. However, with the
potential growth of modules the approach may be overlooked in favor of
an module settings table that will hold key/value rows suitable for the
use by any modules in a unified way.

&#8617; [Home](https://github.com/RecessMobile/API)
--------------
