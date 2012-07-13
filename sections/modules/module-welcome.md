Welcome module is intended to send Welcome responses to the first-time
users of SMSCs or applications.

This module works on two levels: SMSCs and Applications. In most cases,
responses belong to a specific application and they will be passing
through the application-level module. In rare cases, when the message is
not associated with any application, the module of the SMSC it came
through will be working with it.

This module doesn’t stop the processing of the message. It sends the
welcome message (if entered) in addition to the further processing which
may or may not result in any additional messages.

Configuration:

-   Welcome text message - the message to send. If the message is not
    given, the module is inactive. The message field can be found on the
    application and SMSC edit page in the administrative console.
