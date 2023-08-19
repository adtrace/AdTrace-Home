# FAQs for AdTrace Android Webbridge SDK

---
## General Questions
### My application is just one activity with a single `web-view` inside of it. how AdTrace is going to work on a web page inside of an app?
when an android app is actually a `web-view` loading inside an activity AdTrace is able to work without a problem just like a `native` app. the solution presented is a "Web-Bridge".

AdTrace "Web-Bridge" simply acts like a bridge between android and web sides of application. `native sdk` is the base for sending and managing connection and data, while `web-bridge sdk` is just an interface accessible via the web side of the app.

initialization is available both from web side or android native side. if your app starts from the web (meaning that user first interacts with the web page layout) use [web side initialization](https://github.com/adtrace/adtrace_sdk_android#web-views-sdk). if your app starts from android native activity and some the pages are web view (which means user first interacts with android layout and may or may not enter web pages from there) use [android native initialization](https://github.com/adtrace/adtrace_sdk_android#native-app-sdk).

other than initialization some features may need to implement too. for instance you want to [trigger an `event`](https://github.com/adtrace/adtrace_sdk_android#track-event) when user clicks on a certain button or you want to [set firebase push token](https://github.com/adtrace/adtrace_sdk_android#push-token). in these cases you need to use whichever side (web view or native) you target to implement.


---
## Implementation