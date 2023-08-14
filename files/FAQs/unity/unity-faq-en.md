# FAQs for AdTrace Unity SDK

---
## General Questions



---
## Implementation

### I want to send custom parameters with `AdTrace-SDK`. what should I do?
AdTrace provides `Event` as a set of parameters which you can trigger where ever you want in your app. for example whenever the user clicks on a button to purchase something you can set an `Event` to be triggered.

However, sometimes you want to add some parameters like what user wanted to purchase or how much it was. for this purpose you can use `eventValueParams` , to add unlimited `key` and `value` pairs to the event.
