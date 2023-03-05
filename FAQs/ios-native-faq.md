# FAQs for AdTrace iOS native SDK




---
## Basic implementation
This part is necessary for the basic functionality of the SDK. Each step **MUST** be done.

---

## Add Adtrace to your project

[official documentation](https://github.com/adtrace/adtrace_sdk_iOS#basic-integration)

### Where can I see real Examples of implementation?

### Can I use Adtrace for `swift` projects too?

### How to use `SPM` instead of `pods`?

### Does Adtrace provides `xcframework`?

### Where can I get Adtrace `xcframework` files?

### Where can I find `app token`?

### I don't see any `log` from Adtrace!

### I don't see any changes in Adtrace panel statistics!

### Why there is no change in installs even when I remove and install the app again?

### How to make sure everything is working fine (as expected)?

---
## Adtrace Tracking Transparency

[official documentation](https://github.com/adtrace/adtrace_sdk_iOS#apptrackingtransparency-framework)

### Adtrace makes my app ask for tracking authorization

### How to disable tracking authorization?

### How do I know if user allowed app-tracking authorization?


---
## Event tracking

[official documentation](https://github.com/adtrace/adtrace_sdk_iOS#event-tracking)

#### What is `eventToken`?
AdTrace Event is identified using a string token. this token is a set of characters and does not represent any meaning. when you create an event in [AdTrace panel](https://panel.adtrace.io) you'll access to it's token with which you can define an event to trigger.

#### What is a `unique` event?
An unique event is an event which will be received only one in app life time. this is used for actions that occur once (e.g. account creation). nothing need to be implemented from SDK side and it is only can be set from panel when event is created. 

#### How many events per user (or per certain amount of time) you can track?
There is no limit. you can send any number of events any period of time with any time interval between them.

#### How many different events can you define?
Technically there is no limit to the number of different events you can define in AdTrace panel. how ever as a rule of thumb, more than few events for an application probably is not the best way to collect data to analyze. don't confuse too much different events with high number of event calls. to be more clear take a look at following example for a set of events:

:x: case 1:
```
event 1: purchase_cloth
event 2: purchase_hat
event 3: purchase_watch
event 4: purchase_glass
...
event 99: ...
```

:white_check_mark: case 2:
```
event 1: purchase
event 2: open_page
event 3: add_to_cart
event 4: share
```


case 2 (exaggerated) is not optimum. make sure to check all the event capabilities and options.

#### How to make sure event is successfully sent?
After each event is send, there are callbacks for both successful or failed request. for more information about how to set event tracking listeners [see this](https://github.com/adtrace/adtrace_sdk_android#session-and-event-callbacks).

You can [take a look at Logs while testing](#how-to-configure-adtrace-for-testing) too.

---

### Revenue

#### Does AdTrace converts revenues considering currency name?
No. the currency name that you add to your revenue is just separates those values preventing them from mixing. however it is better for your data to be send using single currency like `Tooman`, `Rial` or `Dollar`.

*Remember DO NOT send revenue data through event value parameters*

---

### Revenue deduplication

#### Why Revenue deduplication is important and how to use it?
Mostly event revenue is considered as a source to compare real revenue from in app purchase or similar methods. this data is must be carefully treated and when large number of users are purchase sometimes data collected from different sources (e.g. AdTrace revenue vs real financial data from bank) are saying different things.

The main cause of this issue is rooted in the process of events. when user presses the purchase button, due to connection delays for instance, application does not response immediately and user temps to press the button several time. this leads to triggering few events for one purchase. as AdTrace promises to send any number of events within any interval of time, it will do. that would be a problem when event has revenue and for a single purchase AdTrace receives several revenues.

To prevent this from happening, AdTrace suggests revenue deduplication. when you want to trigger an event with revenue, consider a unique `OrderId` for that purchase for each, so that if this event triggered more than once, AdTrace knows it is the same and prevent it from adding to your overall revenue. for more information about [how to prevent revenue duplication](https://github.com/adtrace/adtrace_sdk_android#et-revenue-deduplication) see this part of docs.

---

### Value parameters

#### How can I add any information that I want to event?
As an event is a golden source of users analytics, some times it is necessary to send related information that are even more important. on the other side you can not define an event for each single case in the application.

You can add any value to an event using value parameter. this parameters are `key`,`value` and `String` based. after adding any amount of value parameters, the event is send as a regular simple event. for more information [see this](https://github.com/adtrace/adtrace_sdk_android#event-parameters-1).

#### How many parameters can be added to event?
There is no limit to this. you can have any number of parameters added to event. how ever the best practice is to consider a structure for your events. more like a default keys with their values changing for each event. see this example:

:x: case 1:
```
event 1:
  {
    "first_name":"John", 
    "last_name":"brown",
    "time":"15:49PM" // events already contain exact time and date
   } 

event 2:
  {
    "name":"John Brown",// default format missed
    "cost":"1000$", // never use revenue in value parameters
    "date":"10-8-2021" // events already contain exact time and date
  }
```

:white_check_mark: case 2:
```
event 1:
  {
    "name":"John Brown",
    "item_type":"mobile",
    "item_name":"Samsung Galaxy S23 Ultra",
    "item_color":"Lime",
    "user_id":"123456789"
    ...
   } 

event 2:
  {
    "name":"Sara Wills",
    "item_type":"keyboard",
    "item_name":"Keychron Q6",
    "item_color":"Dark",
    "user_id":"987654321"
    ...
   } 
```

This way collected data is clean, ready and unnecessary or duplicated information is not added.

---

## Session

### How should I send a session?

### How to make sure session is successfully sent?


