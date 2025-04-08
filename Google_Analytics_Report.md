# 📊 Differences Between Universal Analytics and Google Analytics 4

This document outlines the key differences between the older Universal Analytics (UA) and the newer Google Analytics 4 (GA4).

You also have access to a [comparative table](./Table.md)

## ⚙️ Data Model:

- **Universal Analytics (UA):** The event model is session-based.
- **Google Analytics 4 (GA4):** The data model is event-based.

![img](https://blog.markezing.com/hs-fs/hubfs/UA%20and%20GA%20data%20collection.png?width=832&height=616&name=UA%20and%20GA%20data%20collection.png)While it may take longer to implement, the data will be more targeted, leading to more explicit answers. GA4's model is highly flexible, but this doesn't necessarily mean UA is less performant.

## 🔒 Privacy and GDPR Compliance:

With the arrival of GDPR regulations, many organizations had to discard data to respect the choices of internet users who refused data tracking.

With Google Analytics 4, Google has adopted a new way of collecting and tracking data while respecting current privacy regulations.

## 📈 Adjusted Data Limits:

In Universal Analytics, each tracking event is sent as an individual image tag to Google's servers. With the older version of Google Analytics, an e-commerce site sending data on all page views, interactions, and product impressions could place a significant load on Google's servers. Consequently, Google historically imposed access limits on the free version of Universal Analytics.

Examples of limits for the free Universal Analytics offering:

- 10 million hits per property
- 200,000 hits per user per day
- 500 hits per session

These limits no longer apply to new GA4 properties.

GA4 uses a queuing system developed by Google so that multiple events can be grouped into the same network request, meaning less load on Google's servers.

However, there are other limitations to be aware of in GA4. Google has imposed various limits on the number of distinct events you can track and the number of parameters per event, as well as the character length of these parameters.

## 🧪 Sampling:

Sites with high traffic volume will eventually trigger "sampling" when you make a request that combines dimensions and metrics in a way that cannot be extracted from pre-aggregated tables. Sampling serves to balance Google's ability to calculate complex reports while avoiding excessive use of computing resources.

The drawback of sampling is the sample size itself. Google Analytics Universal sometimes bases its calculations on as little as 1% of your actual data. If this 1% of data is not truly representative of the complete data capture, your data reporting will present a very biased view of reality.

With GA4's event-based data model and user interface restrictions, sampling should be less problematic, but Google plans to provide more details on GA4 sampling later.

## 🛡️ Prevention and False Data:

Spam referrals are a common data accuracy issue in Google Analytics Universal. With only the Universal Google Analytics property ID, it is easy for malicious actors to populate someone's Google Analytics property with spam data using the Measurement Protocol.

Google has now made this virtually impossible with GA4 by forcing Measurement Protocol calls to include a secret key that is visible in the GA4 Web data stream settings but is not publicly available. Only calls with a valid key can send data to a GA4 property.

You can access the Measurement Protocol API key in the "Additional Settings" section of a GA4 Web data stream.

## 👤 User Identification:

User identification has undergone a significant update. In the current Universal Analytics property, a default view reports anonymous/unknown traffic that has been identified with the anonymous Client ID, which is automatically read from the `_ga` cookie.

If your website includes a login state, you can then create a separate view that reconciles users based on the User ID value exposed in your data layer and populated in Google Analytics for authenticated users.

This approach is not always ideal as it does not provide a single view of your data to leverage the multiple identifiers that can be used to unify separate sessions between individual users. User ID-based views do not recognize the Client ID and sometimes do not generate much data.

Google Analytics 4 instead leverages a "fallback" approach with multiple methods to identify or deduplicate unique users:

- **User ID:** GA4 will first check if you have passed a User ID value that represents authentication on your own back-end and that you have typically exposed on your website's data layer.
- **Google Signals:** If the User ID is available, GA uses Google Signals, which is linked to a Google login. You need to [enable Google Signals](https://support.google.com/analytics/answer/9445344?hl=fr) in your GA4 property.
- **Client ID:** If nothing has been detected so far, GA4 defaults to using the Client ID (the `_ga` cookie).

## ⏳ Sessions in the New Google Analytics 4:

Currently, Universal Analytics will increment a session with one of these scenarios:

- **Time-based expiration:** 30 minutes of inactivity or at midnight.
- **Change of source, medium, or campaign dimensions.**

In GA4, a `session_start` event will trigger at the beginning of each new session. If 30 minutes have passed without the user generating any events, the next event generated by the user will automatically generate a new `session_start` event.

This approach to calculating sessions in GA4 is comparable to the basic session calculation logic in Universal, but the other factors in Universal that also trigger a new session (changes in day or traffic acquisition dimensions) no longer apply. For this reason, GA4 may show fewer sessions than Google Analytics Universal for the same user interactions.

## 🏷️ Content Grouping:

Content Grouping reports are not available in the new Google Analytics 4. This reporting feature closely corresponds to hit-scoped custom dimensions in Google Analytics Universal.

In Google Analytics 4, you can leverage event parameters and custom dimensions to essentially reproduce the content groupings we know from GA Universal.

## 📏 Custom Metrics:

In Google Analytics Universal, you can directly capture custom metrics, meaning you send numerical data with an event or pageview hit explicitly as a custom metric.

Similar to Google Analytics 4 custom dimensions, it is the mapping of an event parameter that determines whether it will be treated as a custom metric.

In the All Events report, you can map this event parameter as a custom metric to be incremented each time a user generates a GA4 event containing that parameter.

## 👓 Views:

GA4 does not offer a special "Views" functionality. Reporting occurs at the property level, which is essentially your main view. For example, there is no equivalent method to isolate traffic from your blog from your main site.

Views provided the ability to resolve data issues, reduce cardinality, create roll-up views, and apply filters. All these features are now missing in Google Analytics 4.

It is expected that Google will address views through a new set of features, but these may only be offered to users of the paid version.

## ✨ Enhanced Measurement:

GA4 has made the most common tracking available out-of-the-box with little to no configuration required.

In Universal Analytics, enhanced measurement tracking typically required custom GTM (Google Tag Manager) setup, but it is now standard for all GA4 properties.

## 🎯 Conclusion:

As mentioned earlier in this article, GA4 refocuses on user logic. Thus, for GA4, there is more value in analyzing an engagement rate than a bounce rate.

Google Analytics 4 announces an unprecedented evolution in the approach to analytics. It is therefore important to adapt to this new model and switch to Google Analytics 4 now. However, we advise you to **keep your Universal Analytics account in parallel initially.** This will allow you to compare your data and give you more time to set up the tracking adapted to your needs.

Google Analytics 4 has completely revised its data model to be in line with the changes that have occurred in recent years (mobile application and GDPR). Google has taken the opportunity to enrich this new version to simplify certain aspects and offer **new tracking possibilities.**

However, although **GA4 is still cookie-based**, AI is supposed to be able to compensate for data losses related to this operation. In addition, all these new possibilities require more complex tagging in GTM (Google Tag Manager).

Getting to grips with this new version is also more complex, but the template gallery that is made available should expand rapidly to simplify this task in the future.
