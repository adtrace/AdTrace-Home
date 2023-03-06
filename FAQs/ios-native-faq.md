# FAQs for AdTrace iOS native SDK




---
## Basic implementation
This part is necessary for the basic functionality of the SDK. Each step **MUST** be done.

---

## Add Adtrace to your project

[official documentation](https://github.com/adtrace/adtrace_sdk_iOS#basic-integration)

### Where can I see real Examples of implementation?
[Adtrace official github](https://github.com/adtrace/adtrace_sdk_iOS) includes several examples for different cases.

[ObjC Project example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-ObjC)
[Swift Project Example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-Swift)
[WebView Project Example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-WebView)
[iMessage Project Example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-iMessage)
[iWatch Project Example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-iWatch)
[tvOS Project Example](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples/AdtraceExample-tvOS)

### Can I use Adtrace in my `swift` projects too?
Yes for short answer, for more information [see this](https://github.com/adtrace/adtrace_sdk_iOS#basic-integration)

### How to use `SPM` instead of `pods`?
You can add Adtrace iOS SDK using [official github repository](https://github.com/adtrace/adtrace_sdk_iOS). simply go to `File > Add Packages...`. enter url for iOS SDK repository (e.g. `https://github.com/adtrace/adtrace_sdk_iOS`) for `Package URL`.

### Does Adtrace provides `xcframework`?
Yes, there is a stack of frameworks after each release in [official github repository for iOS SDK](https://github.com/adtrace/adtrace_sdk_iOS/releases). there is also [build script](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/script) for building frameworks.


### Where can I find `app token`?
After creating an account in [Adtrace panel](https://pnael.adtrace.io) you can create an application. by creating an app, Adtrace will generate a hash-like `app token` which you can use it in your app as String which indicates your application for our backend. you can find it in `Panel > Settings > AppToken`.

### I don't see any `log` from Adtrace!
Adtrace generally prints logs in different levels. for more information [see this](https://github.com/adtrace/adtrace_sdk_iOS#adtrace-logging). make sure to set up logging level you wish to. in order to see all the logs from Adtrace SDK set log level to `Verbose`. *note that if [Adtrace Environment](https://github.com/adtrace/adtrace_sdk_iOS#basic-setup) is set to `ADTEnvironmentSandbox` all the logs are dismissed. to activate logs instead use `ADTEnvironmentSandbox`.*

### I don't see any changes in Adtrace panel statistics!
When SDK is properly integrated to your app it'll sends data to our backend and those data will be shown. if you don't see any changes in statistics make sure to check following cases:

- [Minimum requirement is not provided for SDK to work]()
- [Adtrace Panel is not configured correctly]()
- [The Device is detected before]()
- [Make sure everything is working fine (as expected)]()

### What is the minimum requirement for Adtrace SDK?
Adtrace provides a plentiful stack of features and you may want to use all or a part of them. however in order for Adtrace SDK to provides analytics and statistics for your application you MUST integrate [basics](https://github.com/adtrace/adtrace_sdk_iOS#basic-integration).

First make sure following parts are done:
- [Add SDK to your project](https://github.com/adtrace/adtrace_sdk_iOS#add-the-sdk-to-your-project)
- [Integrate the SDK into your app](https://github.com/adtrace/adtrace_sdk_iOS#integrate-the-sdk-into-your-app)
- [Basic setup](https://github.com/adtrace/adtrace_sdk_iOS#basic-setup)

you can always take look at [example apps](https://github.com/adtrace/adtrace_sdk_iOS/tree/master/examples) without hesitation.


### Sandbox mode vs Production mode
When you are started to integrate Adtrace into your app or you're about to test if it is working as expected you have to set [Adtrace Environment](https://github.com/adtrace/adtrace_sdk_iOS#basic-setup) to `ADTEnvironmentSandbox`. this way traffic from testing is separated from `ADTEnvironmentProduction` which is used for release and SDK will prints logs too in order you to see it's functionality. make sure to change it back to `ADTEnvironmentProduction` before release.

Note that you can control amount of logs using [log level](https://github.com/adtrace/adtrace_sdk_iOS#adtrace-logging) however it is recommended to set it to `Verbose` to see all.

### How to make sure everything is working fine (as expected)?
Prior to all other functionalities Adtrace needs application to be opened and an `Install` occurs for the application on the Device.

- [How do I know if `Install` is tracked?]()
- [How do I know if `Session` is tracked?]()
- [How do I know if `Event` is tracked?]()

### How do I know `Install` is tracked?
There are two ways to check if `Install` is tracked.

- [Check if `Install` is tracked via `Log`]()
- [Check if `Install` is tracked via `Testing Console`]()


### Check if `Install` is tracked via `Log`
Firstly, make sure you're in Sandbox mode.

When SDK printed logs, simple search for `response` which our backend is sends back to SDK requests. if the `response` object contains `adid` field with hash-like value, `Install` is tracked.  


### Check if `Install` is tracked via `Testing Console`
First go to `Settings > Testing Console` in [Adtrace Panel](https://panel.adtrace.io).

You need to provide an ID referring to the Device to check if `Install` is tracked. if your application is authorized to obtain `IDFA` then you can use it, otherwise you have to search for `primary_dedupe_token` use it's value as `IDFA`.

### What is a "Fresh Device"?
When an application is `Install`ed on a device, it'll be known and if the application is uninstalled and install again, it won't be considered as a new `Install`. this is a problem when testing installs because you need to use a device which is not recorded before for the app, or a "Fresh Device". 

### How to "Forget" my device?
Go to [Adtrace panel](https://panel.adtrace.io). follow the path `Settings > Testing Console`. enter your Device's ID to clear it's information from Adtrace backend.

### Is Panel configured for what I want to see?
When viewing data and statistics in Adtrace panel, you might consider following cases to make sure every thing is shown as you wish to:
- Locale time
- Selected Interval
- Fraud Detection Settings
- Filtering

### Why there is no change in installs even when I remove and install the app again?
As an app is installed on a device, that device will be known to Adtrace for the app and if you reinstall an app right after installing, it will not considered as a new install. for more information see [Fresh Device]() and [Forget Device]().
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


