Subscriptions module when enabled controls whole cycle of subscription
management and enables the applications to use subscription
registration, tagging and message sending.

The module monitors incoming messages for the keywords and processes
them when detected without passing the messages to the client
applications. Keywords and responses to them are entered in the
Subscription Configuration on per-application basis.

All subscribers are registered in the Subscriptions table and can be
tagged by the client application for the purpose of grouping.

Configuration:

-   Subscription Keywords - space-separated list of keywords that
    indicate the subscription request (default, SUB)
-   Subscription Message - message to return the user on successful
    subscription (default, Subscribed to [STORE] special offers. Up to
    5/mo. Std msging rates & other charges may apply. Cancel, reply
    STOP, for help, HELP. T&Cs: [LINK])
-   Confirmation Keywords - space-separated list of keywords that
    indicate the confirmation of the subscription request for AT&T users
    (default, Y)
-   Confirmation Message - message to return when the subscription
    confirmation is required (default, [STORE] special offers - up to
    5/mo. Txt Y to accept. Other charges may apply. Cancel, reply STOP,
    for help, HELP. T&Cs: [LINK])
-   Cancellation Keywords - space-separated list of keywords that
    indicate the cancellation of the subscription (default, STOP END
    QUIT CANCEL UNSUBSCRIBE)
-   Cancellation Message - message to return when the subscription is
    canceled (default, You’ve canceled your subscription to [STORE]
    special offers. You will not receive any more messages. More, visit
    [LINK])
-   Unsubscribed Cancellation Message - message to send when the
    cancellation request is sent by an unsubscribed user (default, Your
    subscription to [STORE] special offers is canceled. You will not
    receive any messages. More, visit [LINK])
-   Renewal Keywords - message to send when the subscription is renewed
    (default, Renewed: Subscribed to [STORE] special offers. Up to 5/mo.
    Std msging rates & other charges may apply. Cancel, reply STOP, for
    help, HELP. T&Cs: [LINK])
-   Limit - number of subscription message per Limit Period that are
    allowed to this application (default, 5)
-   Limit Period - period of the limit (day, week, month etc)
