Module - static responses
=========================

Static responses module provides an extremely flexible feature -
automated responses to certain keywords - to client applications or
SMSCs in general. Static responses are stored in the table where
keywords are associated with responses.

When an MO arrives, its contents are checked against the table associated
with the target application (or with SMSC it came through if no
application is currently associated with the phone number). If the
message finds its response, the client application never receives it,
but instead the MT is sent automatically.

An application or SMSC can have any number of static responses that can
be registered through the application (or SMSC) details page. Every
message can have the Free flag set which means that the response has to
be sent as an FTEU message.

Configuration
-------------

**Keyword-Response** pairs can be entered on the application/SMSC details page


&#8617; [Home](https://github.com/RecessMobile/API)
--------------