# FAQs for AdTrace Android Webbridge SDK

---
## General Questions
### My application is just one activity with a single `web-view` inside of it. how AdTrace is going to work on a web page inside of an app?
when an android app is actually a `web-view` loading inside an activity AdTrace is able to work without a problem just like a `native` app. the solution presented is a "Web-Bridge".

AdTrace "Web-Bridge" simply acts like a bridge between android and web sides of application. `native sdk` is the base for sending and managing connection and data, while `web-bridge sdk` is just an interface accessible via the web side of the app.

initialization is available both from web side or android native side. if your app starts from the web (meaning that user first interacts with the web page layout) use [web side initialization](https://github.com/adtrace/adtrace_sdk_android#web-views-sdk). if your app starts from android native activity and some the pages are web view (which means user first interacts with android layout and may or may not enter web pages from there) use [android native initialization](https://github.com/adtrace/adtrace_sdk_android#native-app-sdk).

other than initialization some features may need to implement too. for instance you want to [trigger an `event`](https://github.com/adtrace/adtrace_sdk_android#track-event) when user clicks on a certain button or you want to [set firebase push token](https://github.com/adtrace/adtrace_sdk_android#push-token). in these cases you need to use whichever side (web view or native) you target to implement.


### Can `Web-Bridge` have the exact same functionality as native?
yes. any interface you have been using in native, you can use it from web side. in fact each part of the [android documentation](https://github.com/adtrace/adtrace_sdk_android) is consist of both android native and `Web-view` sample of implementation.


### Can I use AdTrace for `PWA`?
if you have a `Progressive Web Applications` you can use [AdTrace `Web SDK`](https://github.com/adtrace/adtrace_sdk_web). if you are using it inside of an android application then you need to implement AdTrace android and web view SDKs.

### Can I use AdTrace for `TWA`?
`Trusted Web Activity` is also supported by AdTrace. make sure to contact our support for more information.


---
## Implementation

### Do I need to add any "SDK" or scripts to web side?
yes. AdTrace needs to keep its data structure same and untouched through out all the processes. in order to do that you need to import asset file of `Web-Bridge`.

### I am using the same project and source for android `Web-View` and `PWA`. is AdTrace able to track my data using just `Web-Bridge` SDK?
there is not any conflict for using both AdTrace `Web-Bridge SDK` and `Web SDK` in one project. the only important consideration is separating them, meaning to use `Web-Bridge SDK` scripts when webview is loaded inside the app and `Web SDK` when loaded on a browser. 

### Which files I need to import for web side?
you need to import `js` asset files to your web project in order for AdTrace to work with same data structure regarding web and native sides. this is done simply by adding [these files](https://github.com/adtrace/adtrace_sdk_android/tree/master/android-sdk-plugin-webbridge/src/main/assets) to the project and following [documentation](https://github.com/adtrace/adtrace_sdk_android).

### I need real world sample projects.

- [android Web Bridge Example](https://github.com/adtrace/adtrace_sdk_android/tree/master/example-app-webbridge)
- [Web Side Example: Next.js](https://github.com/adtrace/nextjs-webview)
- [Web Side Example: Next.js 2](https://github.com/adtrace/nextjs-example)

### Which platforms AdTrace supports for using `Web-Bridge`?
all popular platforms.

### How many `event`s my app can send in a day? how many parameters or meta data each `event` can have?
see these: 
- [number of events you can define](./android-native-faq-en.md/#how-many-different-events-can-you-define)
- [number of events limitations](./android-native-faq-en.md/#how-many-events-per-user-or-per-certain-amount-of-time-you-can-track)

### I am not sure if AdTrace is tracking all of my `event`s. what can I do?
see this: [Event Tracking Testing](./android-native-faq-en.md/#how-to-make-sure-event-is-successfully-sent)