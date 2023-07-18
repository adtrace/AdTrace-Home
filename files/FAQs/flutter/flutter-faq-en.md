# FAQs for AdTrace Flutter SDK

- [FAQs for AdTrace Flutter SDK](#faqs-for-adtrace-flutter-sdk)
  - [General Questions](#general-questions)
    - [which platforms are supported in flutter sdk?](#which-platforms-are-supported-in-flutter-sdk)
    - [are there any difference between android or iOS SDKs and flutter SDK?](#are-there-any-difference-between-android-or-ios-sdks-and-flutter-sdk)
  - [Implementation](#implementation)
    - [how to find flutter SDK for Adtrace?](#how-to-find-flutter-sdk-for-adtrace)
    - [I need specific version of flutter SDK, how can I find it?](#i-need-specific-version-of-flutter-sdk-how-can-i-find-it)
    - [why do I don't see any data on Adtrace dashboard even though I have integrated Adtrace Flutter SDK?](#why-do-i-dont-see-any-data-on-adtrace-dashboard-even-though-i-have-integrated-adtrace-flutter-sdk)
    - [I have problem receiving `deferred deeplink`.](#i-have-problem-receiving-deferred-deeplink)
    - [install tracking is NOT working in `production` mode, but works in `sandbox`.](#install-tracking-is-not-working-in-production-mode-but-works-in-sandbox)
    - [`Could not build module 'adtrace_sdk'`](#could-not-build-module-adtrace_sdk)


---
## General Questions

### which platforms are supported in flutter sdk?
iOS,android!

### are there any difference between android or iOS SDKs and flutter SDK?
no there is not! flutter SDK is based on native android and iOS SDKs of Adtrace.



---
## Implementation

### how to find flutter SDK for Adtrace?
there are several ways!
first consider searching on [`pub.dev`](https://pub.dev) website and search for `adtrace`.

[https://pub.dev/packages/adtrace_sdk_flutter](https://pub.dev/packages/adtrace_sdk_flutter)

consider adding latest version of SDK to your project.

### I need specific version of flutter SDK, how can I find it?
Adtrace flutter [SDK releases](https://github.com/adtrace/adtrace_sdk_flutter/releases) are listed in [official github repo](https://github.com/adtrace/adtrace_sdk_flutter) for it.


### why do I don't see any data on Adtrace dashboard even though I have integrated Adtrace Flutter SDK?
There're may be several reason why you can not see any data on the dashboard. we will be going through them one by one.
- **Reason**: SDK is not or partly integrated into the application.
- **Solution**: make sure to double check documentation carefully (both native side and `dart` code), if you still have the issue contact our support.
- **Reason**: dashboard settings are not what you intend to see.
- **Solution**: make sure to check time, type of data and fraud related settings. if you have any questions contact our support.


### I have problem receiving `deferred deeplink`.
When testing deferred deep linking (and at the end of the test seeing deferred deep link callback triggered in the app), you need to make sure to have testing flow set up properly. That involves following:

1. Make sure that tracker URL you're testing with is properly formatted.
2. In case you are not using your test device ID as part of the tracker URL, make sure to have probabilistic matching enabled for the test tracking in the dashboard settings.
3. Uninstall your app from test device.
4. Forget your test device from our backend via testing console.
5. Click on a tracker URL from from some page you loaded in your test device browser.
6. Ignore the redirection to App/Play Store.
7. Install app on your test device and launch SDK (preferably in sandbox mode and with log level set to verbose so that you can see what's happening in the logs).
8. If all went well, you should see install being tracked + deferred deep link sent back to SDK + deferred deep linking callback you have defined being pinged by the SDK.
In case you end up having any further questions about this flow, feel free to contact us.

### install tracking is NOT working in `production` mode, but works in `sandbox`.
if you're is using any kind of **obfuscation**  (ProGuard, R8 and etc) sometime it can cause things to break down. to prevent this from happening make sure to consider [this part of documentation carefully](https://github.com/adtrace/adtrace_sdk_flutter#qs-proguard) for using Adtrace SDK.

### `Could not build module 'adtrace_sdk'`
go to `Build Settings` under `Target` and set `Allow Non-modular Includes in Framework Modules` to `YES`.

