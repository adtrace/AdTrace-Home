# FAQs for AdTrace android native SDK

**table of contents**
- [FAQs for AdTrace android native SDK](#faqs-for-adtrace-android-native-sdk)
  - [Basic implementation](#basic-implementation)
    - [Add AdTrace Sdk to the project](#add-adtrace-sdk-to-the-project)
      - [I keep seeing `"packge not resolved"`](#i-keep-seeing-packge-not-resolved)
      - [Which version of SDK should I use?](#which-version-of-sdk-should-i-use)
      - [What if I use a deprecated version?](#what-if-i-use-a-deprecated-version)
      - [I don't want to use Maven Central.](#i-dont-want-to-use-maven-central)
    - [Add AdTrace Dependencies](#add-adtrace-dependencies)
      - [Add Google Play Services](#add-google-play-services)
      - [What if I don't add this library?](#what-if-i-dont-add-this-library)
    - [Add Install Referrer](#add-install-referrer)
      - [What if I don't add this library?](#what-if-i-dont-add-this-library-1)
      - [Can I remove `AdTraceReceiver` in `AndroidManifest.xml` file?](#can-i-remove-adtracereceiver-in-androidmanifestxml-file)
    - [Add Permissions](#add-permissions)
      - [Google Play Store rejected new update due to `AD_ID` permission](#google-play-store-rejected-new-update-due-to-ad_id-permission)
    - [Basic Setup](#basic-setup)
      - [Can I see information on AdTrace Panel while using `Environment.SandBox`?](#can-i-see-information-on-adtrace-panel-while-using-environmentsandbox)
      - [I already have a class that extends `Application`, Do I have to create another?](#i-already-have-a-class-that-extends-application-do-i-have-to-create-another)
      - [What is the minimum requirement for AdTrace to work?](#what-is-the-minimum-requirement-for-adtrace-to-work)
      - [Is calling `AdTrace.onCreate` enough to send `Install`?](#is-calling-adtraceoncreate-enough-to-send-install)
    - [How to make sure everything is working fine (as expected)?](#how-to-make-sure-everything-is-working-fine-as-expected)
      - [How to configure AdTrace for testing?](#how-to-configure-adtrace-for-testing)
      - [What is a "Fresh Device"?](#what-is-a-fresh-device)
      - [How to "Forget" a device?](#how-to-forget-a-device)
      - [How to get my `device ID`?](#how-to-get-my-device-id)
  - [Deep linking](#deep-linking)
    - [Standard deep linking scenario](#standard-deep-linking-scenario)
      - [How can I define deeplink for AdTrace?](#how-can-i-define-deeplink-for-adtrace)
    - [Deferred deeplinking scenario](#deferred-deeplinking-scenario)
      - [What is deferred deeplink?](#what-is-deferred-deeplink)
      - [Do I need to define a different type of deeplink for this?](#do-i-need-to-define-a-different-type-of-deeplink-for-this)
      - [Is it necessary to configure SDK for deeplinking?](#is-it-necessary-to-configure-sdk-for-deeplinking)
    - [Reattribution via deep link](#reattribution-via-deep-link)
  - [Event Tracking](#event-tracking)
    - [Event](#event)
      - [What is `eventToken`?](#what-is-eventtoken)
      - [What is a `unique` event?](#what-is-a-unique-event)
      - [How many events per user (or per certain amount of time) you can track?](#how-many-events-per-user-or-per-certain-amount-of-time-you-can-track)
      - [How many different events can you define?](#how-many-different-events-can-you-define)
      - [How to make sure event is successfully sent?](#how-to-make-sure-event-is-successfully-sent)
    - [Revenue](#revenue)
      - [Does AdTrace converts revenues considering currency name?](#does-adtrace-converts-revenues-considering-currency-name)
    - [Revenue deduplication](#revenue-deduplication)
      - [Why Revenue deduplication is important and how to use it?](#why-revenue-deduplication-is-important-and-how-to-use-it)
    - [Value parameters](#value-parameters)
      - [How can I add any information that I want to event?](#how-can-i-add-any-information-that-i-want-to-event)
      - [How many parameters can be added to event?](#how-many-parameters-can-be-added-to-event)
  - [Session](#session)
    - [How should I send a session?](#how-should-i-send-a-session)
    - [How to make sure session is successfully sent?](#how-to-make-sure-session-is-successfully-sent)
  - [Additional topics](#additional-topics)
    - [Uninstall (push token)](#uninstall-push-token)
      - [What is required for AdTrace in order to track uninstall?](#what-is-required-for-adtrace-in-order-to-track-uninstall)
      - [What is Silent push?](#what-is-silent-push)
      - [Why my app receives unwanted notifications without any content?](#why-my-app-receives-unwanted-notifications-without-any-content)
    - [Attribution ](#attribution)
      - [How to receive attribution data?](#how-to-receive-attribution-data)
      - [How long will it takes for attribution for be received?](#how-long-will-it-takes-for-attribution-for-be-received)
    - [Device IDs](#device-ids)
      - [What is `GPS AdId` or `Google Advertising ID` or `Google Play Services Ad ID`?](#what-is-gps-adid-or-google-advertising-id-or-google-play-services-ad-id)
      - [How to get `Google Advertising ID`?](#how-to-get-google-advertising-id)
      - [I keep getting `00000000-0000-0000-0000-000000000000` or `null` for `Google Advertising ID`!](#i-keep-getting-00000000-0000-0000-0000-000000000000-or-null-for-google-advertising-id)
      - [Is there a run time permission for `ADID`?](#is-there-a-run-time-permission-for-adid)
      - [What if I don't want to add the permission?](#what-if-i-dont-want-to-add-the-permission)
      - [Where can I view/reset my advertising id?](#where-can-i-viewreset-my-advertising-id)
      - [Some devices does not support Google Ad Id (e.g. `Huawei`)!](#some-devices-does-not-support-google-ad-id-eg-huawei)


---
##  Basic implementation

This part is necessary for the basic functionality of the SDK. Each step **MUST** be done.

---

###  Add AdTrace Sdk to the project

[**link to official docs**](https://github.com/adtrace/adtrace_sdk_android#add-the-sdk-to-your-project)

#### I keep seeing `"packge not resolved"`

go to official [Maven Central Repository Search](https://search.maven.org/) and search for `io.adtrace` and make sure to check all the information as presented (e.g. version,...).

also make sure to use proper VPN in some cases.

#### Which version of SDK should I use?

Even though it is highly recommended to use the latest version of the SDK, you can use older versions too. Keep in mind that older versions are deprecated from a point later on.

make sure to take a look at [Releases](https://github.com/adtrace/adtrace_sdk_android/releases)

#### What if I use a deprecated version?

The deprecated version of SDK may work fine on your application considering the features you use. However, in order for us to completely support the version you are using, make sure NOT to use deprecated versions.  
as the process of updating and publishing a new version of your app may take a while for the best decision [contact our support](support).

#### I don't want to use Maven Central.

You can use `aar` or `jar` version of SDK for each release. Everything will be the same either way. [you can access here](https://github.com/adtrace/adtrace_sdk_android/releases).

---

### Add AdTrace Dependencies

#### Add Google Play Services

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#add-google-play-services) 

**FAQs**:

#### What if I don't add this library?

The Google Play Services library is used for obtaining advertising information from user's device and if it is missing from your project, AdTrace SDK will still be able to run on your application and without any `Exception`. However, some base functionalities will be lost. So make sure to add it.

### Add Install Referrer

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#install-referrer)

**FAQs**:

#### What if I don't add this library?

The install Referrer library is used for obtaining campaign information from App Stores and if it is missing from your project, AdTrace SDK will still be able to run on your application and without any `Exception`. However, some base functionalities will be lost. So make sure to add it.

#### Can I remove `AdTraceReceiver` in `AndroidManifest.xml` file?

Google [has announced](https://android-developers.googleblog.com/2019/11/still-using-installbroadcast-switch-to.html) deprecation of `INSTALL_REFERRER` intent usage to deliver referrer information as of March 1st 2020.

You should capture the Google Play Store `INSTALL_REFERRER` intent with a broadcast receiver. If you are **not using your own broadcast receiver** to receive the `INSTALL_REFERRER` intent, add `AdTraceReceiver` tag inside the `application` tag in your `AndroidManifest.xml`.

We use this broadcast receiver to retrieve the install referrer and pass it to our backend. If you are using a different broadcast receiver for the `INSTALL_REFERRER` intent, follow [these instructions](https://github.com/adtrace/adtrace_sdk_android/blob/master/doc/english/multiple-receivers.md) to properly ping the AdTrace broadcast receiver.

### Add Permissions

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#add-permissions)

**FAQs**:

#### Google Play Store rejected new update due to `AD_ID` permission

Google Play Store has recently considered [Families Policies](https://support.google.com/googleplay/android-developer/answer/9893335?hl=en) in publishing apps. According to the new policies, Apps must indicate target audiences prior to publishing. 

> Apps solely targeted to children should not request `AD_ID` permission when targeting Android API 33 or higher. 

If your app targets “children” audiences, you can [remove this permission](https://github.com/adtrace/adtrace_sdk_android#add-permission-to-gather-google-advertising-id) and [enable Google Play Kids option](https://github.com/adtrace/adtrace_sdk_android#af-play-store-kids-apps). otherwise, you can add this permission and inform Google Play Store that you are NOT targeting “children” audiences and [disable Google Play Kids option](https://github.com/adtrace/adtrace_sdk_android#af-play-store-kids-apps).

---

### Basic Setup

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#basic-setup)

**FAQs**:

#### Can I see information on AdTrace Panel while using `Environment.SandBox`?

The SDK will send data to our backend in both `production` and `sandbox` modes. The main purpose is to distinguish between test mode data and real user data. in other words, you can still see data but you can separate them. 

#### I already have a class that extends `Application`, Do I have to create another?

The purpose of adding `AdTrace` to a class extending `Application` is to connect AdTrace initialization to app opening and closing. in other words, AdTrace will start functioning whenever app starts functioning and whenever app stops functioning (e.g. goes into the background) AdTrace will also stops functioning.
according to these, there will be no problem if you already have an `Application` extending class which AdTrace would be added to it, but you MUST add AdTrace init requirements to it. for more information [click here](https://github.com/adtrace/adtrace_sdk_android#basic-setup).

#### What is the minimum requirement for AdTrace to work?

There are numerous capabilities that AdTrace can provide most of which are optional. you can activate depending on your company demands. however you need to implement some of which are required to start basic functionalities.

(assuming [AdTrace dependency libraries](https://github.com/adtrace/adtrace_sdk_android#add-google-play-services) are added to you project) you have to somehow call `AdTrace.onCreate(config)`, `AdTrace.onResume()` and `AdTrace.onPause()` methods in the right place. as `AdTrace.onCreate(config)` depends on `AdTraceConfig` object it is required too on which depends `context`, `appToken` and `Environment`. for more information [click here](https://github.com/adtrace/adtrace_sdk_android#basic-setup).

Now SDK sends `Install` and `Session`.
for more information about adding libraries [see this](#add-adtrace-dependencies).


#### Is calling `AdTrace.onCreate` enough to send `Install`?

Short answer is **NO**. calling this method will set configurations and in order to start AdTrace you have to call `AdTrace.onResume`.


### How to make sure everything is working fine (as expected)?
This is the most important part in integrating AdTrace SDK. there are several ways for you to make sure that SDK implemented and simple works fine. AdTrace SDK reports it's functions via Log and you can observe all in `LogCat` inside android studio or any other way you are comfortable with.

#### How to configure AdTrace for testing?
Firstly you have to set the environment to `AdTraceConfig.ENVIRONMENT_SANDBOX`. **make sure to change it to `AdTraceConfig.ENVIRONMENT_PRODUCTION` before releasing your app**. 
Secondly set your `LogLevel` on `Verbose` to see all AdTrace Logs.
after doing these steps you have to install your app on a [fresh device](#what-is-a-fresh-device) while the device is connected to your PC to receive the logs and check SDK's functionalities.

#### What is a "Fresh Device"?
As an application (containing AdTrace) is installed (and opened) on a device, the SDK initiates and it's state will be stored on it. therefor testing if `Install` is working correctly as expected requires to be a new device.

If you have a new device everything will be fine. incase you to test multiple times and finding a new device might be hard, you can ["Forget"](#how-to-forget-a-device) your current device so that AdTrace backend will detect it.

Not useless to mention, after forgetting the device you have to uninstall and reinstall the app on it (or clear all storage data manually) and open it again.


#### How to "Forget" a device?
When an application (containing AdTrace) opened on a device, AdTrace will assign an unique ID to it so if the app uninstalled and reinstalled again, it does not count a new `Install` and same user is detected.

However when testing it is not the case and you may not want your device to be detected as installed the app before. in that case you can "Forget" you device from AdTrace backend using [AdTrace panel](https://panel.adtrace.io). after logging in to your account follow this path.

`Settings` >> `Testing Console` (left menu) >> enter your `device ID` >> `Forget Device`

there are several `device ID`s you can choose at your comfort. to see how to get you `device ID` [see this](#how-to-get-my-device-id).

#### How to get my `device ID`?
In order to detect a device and prevent fraud on ad campaigns, AdTrace retrieves and assigns several IDs to each device and each app. 

The most important ID is **`Google Advertising ID`** which is generated by Google on Android OS in form of `UUID` refers to `Google AdID`, `Advertising ID`, `GPS AdID` or `Google Play Services AdID`. you can [retrieve it using AdTrace SDK](https://github.com/adtrace/adtrace_sdk_android#af-gps-adid). 

Another important `device ID` is an ID which AdTrace assigns to your app on the device refers to **`AdTrace device identifier`** or `AdTrace adID`. you can [retrieve it using AdTrace SDK](https://github.com/adtrace/adtrace_sdk_android#adtrace-device-identifier) too.

Both of these IDs are exist in AdTrace Log. after [setting AdTrace configuration for testing]() you can find them in printed Log. keywords to search for are `gps_adid` and `adid`. 

examples:
```
gps_adid:   7c67ef26-830e-49b7-8948-b868b19bf4b3

"adid"  :   "mhxd6or7d3u57fnbdy2r4urdrdxr7tlr"
```


---

## Deep linking

### Standard deep linking scenario

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#standard-deep-linking-scenario)


#### How can I define deeplink for AdTrace?
Deeplink is a tool [provided by Android](https://developer.android.com/training/app-links/deep-linking) to pass a certain type of information into your application using a custom link defined by application developer.

As you run a advertising campaign, you may want to pass deeplink through [AdTrace Tracker](https://github.com/adtrace/AdTrace-Home#how-tracker-works) and user redirected to specific page or certain information is passed to the app.

Remember, AdTrace does not change any parameter of your deeplink and you can pass whatever you decided. for more information contact our support.

---

### Deferred deeplinking scenario

[link to official docs](https://github.com/adtrace/adtrace_sdk_android#deferred-deep-linking-scenario)


#### What is deferred deeplink?
As the deeplink is passed to user device, your application must exist on it to receive. if the app was not presented (e.g. user does not installed it yet) this scenario occurs. in this case user redirected to install application and when app opens, deeplink passed to the application even for the first time. for more information [see this](https://github.com/adtrace/AdTrace-Home#how-deferred-deep-linking-works).

#### Do I need to define a different type of deeplink for this?
No. it is only important if you set tracker settings correctly in [AdTrace panel](https://panel.adtrace.io). there is absolutely no difference and deeplink will be received by the app as before. make sure to check [official documentations and examples about deferred deeplink scenario](https://github.com/adtrace/adtrace_sdk_android#deferred-deep-linking-scenario).

#### Is it necessary to configure SDK for deeplinking?
In both scenarios you must configure [AdTrace Tracker](https://github.com/adtrace/AdTrace-Home#how-tracker-works) settings and your app must also [support deeplink](https://developer.android.com/training/app-links/deep-linkin) too. however in **Standard scenario** there is no need to implement any method related to deeplink in SDK but, in **Deferred scenario** you have to [follow the docs](https://github.com/adtrace/adtrace_sdk_android#deferred-deep-linking-scenario) and let the SDK do the rest.


---

### Reattribution via deep link

---

## Event Tracking
[link to official docs](https://github.com/adtrace/adtrace_sdk_android#event-tracking-1)
### Event

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

[link to official documentation](https://github.com/adtrace/adtrace_sdk_android#qs-session-tracking)

### How should I send a session?
As you finish [basic setup](https://github.com/adtrace/adtrace_sdk_android#basic-setup) one of the important parts is [Session tracking](https://github.com/adtrace/adtrace_sdk_android#qs-session-tracking). after implementing related settings, the SDK will do the rest. there is no need any further actions to send session.

### How to make sure session is successfully sent?
After each session that sent automatically by SDK there are callbacks for both successful or failed request. for more information about how to set session tracking listeners [see this](https://github.com/adtrace/adtrace_sdk_android#session-and-event-callbacks). 

You can [take a look at Logs while testing](#how-to-configure-adtrace-for-testing) too.

---

## Additional topics

### Uninstall (push token)

[link to official documentation](https://github.com/adtrace/adtrace_sdk_android#af-push-token)

#### What is required for AdTrace in order to track uninstall?
Basically all you need to do is implement Firebase Messaging Service on your application. AdTrace as many other global attribution tools mainly uses [silent push notification]() for tracking uninstalls. see this for [implementation of firebase](https://firebase.google.com/docs/android/setup).

#### What is Silent push?
As an application uninstalled on a device there is no way to tell if it is uninstalled or it's connection is off. the solution is a push notification which determines the state of app on the device.

To prevent unwanted conflicts with applications push notification system, the notification has no title and body. 

**PLEASE NOTE** that you must check for notification's `title` and `body` and handle presenting it. for more information [take a look at this](https://github.com/adtrace/adtrace_sdk_android#uninstall-tracking).

#### Why my app receives unwanted notifications without any content?
Make sure to handle silent push notifications. for more information [take a look at this](https://github.com/adtrace/adtrace_sdk_android#uninstall-tracking).

---

### Attribution 

#### How to receive attribution data?
After each attribution is received(or changed in some cases) by the SDK, there is a callback for it's data. for more information about how to set attribution listener [see this](https://github.com/adtrace/adtrace_sdk_android#attribution-callback). 

You can [take a look at Logs while testing](#how-to-configure-adtrace-for-testing) too.

#### How long will it takes for attribution for be received?
It is not possible to determine an exact time, however, it depends on connection speed and stability and also less effectively AdTrace servers' traffic,but it is not going to take longer than **few seconds** in worst cases.

If you need to receive attribution data, set your logic in the attribution listener method. whenever the SDK receives that data, it'll passes through that method.

---

### Device IDs
[link to official documentation](https://github.com/adtrace/adtrace_sdk_android#device-ids)

#### What is `GPS AdId` or `Google Advertising ID` or `Google Play Services Ad ID`?
The advertising ID is a unique, user-resettable ID for advertising, provided by Google Play services. for more information [see this](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en).


#### How to get `Google Advertising ID`?
As AdTrace SDK retrieves it, you can receive it from AdTrace SDK. this process is `async` and make sure to not depend your tasks on it without consideration. 

#### I keep getting `00000000-0000-0000-0000-000000000000` or `null` for `Google Advertising ID`!
This can happen due to somehow not having the right access to user's device advertising id. 

A possible case is when user `delete`s their devices id preventing apps from obtaining it.

Another possible case is new changes in android policies including `permission` for advertising id on android 13 and later. android apps must declare `<uses-permission android:name="com.google.android.gms.permission.AD_ID"/>` in the manifest file. 

#### Is there a run time permission for `ADID`?
No.

#### What if I don't want to add the permission?
One of the most important IDs in mobile advertising and analytics is Google Advertising ID. however if you don't add the permission, older versions of android  would still work as before but, in new versions where this permission is needed for obtaining the id, AdTrace can still work as before without problem except the processes that require `ADID`(e.g. reinstall,S2S event) will not be provided.

#### Where can I view/reset my advertising id?
Android device >> `Settings` >> `Google` >> `Ads`

#### Some devices does not support Google Ad Id (e.g. `Huawei`)!
AdTrace supports all android devices including those which use `OAID` or Open Access ID instead. you can add `oaid-plugin` to your project to support this. for more information [see this]().

---