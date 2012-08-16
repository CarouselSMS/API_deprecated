Module - subscriptions
======================

When enabled, the subscriptions module controls whole cycle of subscription management and enables the applications to use subscription registration, tagging and message sending.

The module monitors incoming messages for keywords and processes them when detected. This happens without passing the messages to the your application. Keywords and responses are entered in the application configuration UI, under Subscription Configuration, on per-application basis.

All subscribers are registered in the Subscriptions table and can be tagged into groups by your application.

Other modules
-------------

- ### [General information and introduction](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-general.md)

- ### [Help module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-help.md)

- ### [Static Responses](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-static-respones.md)

- ### ["Welcome" module](https://github.com/CarouselSMS/API/tree/master/sections/modules/module-welcome.md)


Configuration
-------------

-   **Subscription Keywords** -- space-separated list of keywords that
    indicate the subscription request. *Default*: `SUB`
-   **Subscription Message** -- message to return the user on successful subscription. *Default*: `Subscribed to [STORE] special offers. Up to 5/mo. Std msging rates & other charges may apply. Cancel, reply STOP, for help, HELP. T&Cs: [LINK]`
-   **Confirmation Keywords** -- space-separated list of keywords that
    indicate confirmation of the subscription request for users requiring double opt-in. *Default*: `Y`
-   **Confirmation Message** -- message to return when a subscription
    confirmation is required. *Default*: `[STORE] special offers - up to 5/mo. Txt Y to accept. Other charges may apply. Cancel, reply STOP, for help, HELP. T&Cs: [LINK]`
-   **Cancellation Keywords** -- space-separated list of keywords that
    indicate cancelation of a subscription. *Default*: `STOP END QUIT CANCEL UNSUBSCRIBE`
-   **Cancelation Message** -- message to return when the subscription is
    canceled. *Default*: `You’ve canceled your subscription to [STORE] special offers. You will not receive any more messages. More, visit [LINK]`
-   **Unsubscribed Cancelation Message** -- message to send when the
    cancelation request is sent by an unsubscribed user. The body can be the same as a regular Cancelation Message. *Default*: `Your subscription to [STORE] special offers is canceled. You will not receive any messages. More, visit [LINK]`
-   **Renewal Keywords** -- message to send when the subscription is renewed. *Default, Renewed*: `Subscribed to [STORE] special offers. Up to 5/mo. Std msging rates & other charges may apply. Cancel, reply STOP, for help, HELP. T&Cs: [LINK]`
-   **Limit** -- number of subscription messages per Limit Period that are allowed for this application. *Default*: `5`
-   **Limit Period** -- period of the limit (day, week, month, etc.)


&#8617; [Home](https://github.com/CarouselSMS/API)
--------------
