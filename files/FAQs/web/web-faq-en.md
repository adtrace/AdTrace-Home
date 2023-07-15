# FAQs for AdTrace Web SDK

- [FAQs for AdTrace Web SDK](#faqs-for-adtrace-web-sdk)
  - [General FAQs](#general-faqs)
    - [What counts as an install on web?](#what-counts-as-an-install-on-web)
    - [How does attribution work for web?](#how-does-attribution-work-for-web)
    - [Can I set an attribution window for web clicks?](#can-i-set-an-attribution-window-for-web-clicks)
    - [How does reattribution work for web?](#how-does-reattribution-work-for-web)
    - [Can I redirect users to a site address that doesn’t contain the web base URL set in Adtrace’s internal interface?](#can-i-redirect-users-to-a-site-address-that-doesnt-contain-the-web-base-url-set-in-adtraces-internal-interface)
    - [Which of Adtrace’s fraud filters work for web attribution?](#which-of-adtraces-fraud-filters-work-for-web-attribution)
    - [Can I send S2S web attribution events?](#can-i-send-s2s-web-attribution-events)




---
## General FAQs

### What counts as an install on web?
Adtrace counts the first session as an install for web users. When a user reaches the landing page, it is recorded as a conversion. Additional actions are recorded as events.

### How does attribution work for web?
Adtrace does not use an attribution waterfall for web attribution. We use an Adtrace-generated click ID called a reftag for device matching.


### Can I set an attribution window for web clicks?
No, there is no customizable attribution window for clicks. When a user clicks an Adtrace tracker, they are immediately redirected to the page with the web SDK. Unlike with the platform-level app environment, no meaningful gap between click and install occurs.


### How does reattribution work for web?
You can define an inactivity window for reattributions between 0-365 days. This inactivity window is set at the app level, so it applies to all platforms targeted by multi-platform apps.

You can edit the inactivity window at the individual tracker level. This makes it possible to create trackers for web use only, which have a different inactivity window than the parent app setting.

### Can I redirect users to a site address that doesn’t contain the web base URL set in Adtrace’s internal interface?
You can, but Adtrace cannot attribute the user. We use the web base URL to determine whether to append the reftag to a destination URL. If the web base URL is not present, we will not append the reftag and no attribution can be made.


### Which of Adtrace’s fraud filters work for web attribution?
Adtrace uses Anonymous IP filtering for all web attribution data.

### Can I send S2S web attribution events?
Yes! You can send S2S events to Adtrace by including the `adid` or `web_uuid` as the device identifier. If you have access to the same browser storage as our web SDK, you can retrieve the `web_uuid` by querying your backend using javascript. For more information, read about sending S2S events. 