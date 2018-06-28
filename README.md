Notes on practices and patterns specifc to
android development.

### Deep links vs App links

**Deep links** are URLs that take users directly to specific content in your app. In Android, you can set up deep links by adding intent filters and extracting data from incoming intents to drive users to the right activity.

However, if other apps installed on a user's device can handle the same intent, users might not go directly to your app. For example, clicking a URL in an email from a bank might lead to a dialog asking the user whether to use the browser or the bank's own app to open the link.

**Android App Links** on Android 6.0 (API level 23) and higher allow an app to designate itself as the default handler of a given type of link. If the user doesn't want the app to be the default handler, they can override this behavior from their device's system settings.

Android App Links offer the following benefits:

Secure and specific: Android App Links use HTTP URLs that link to a website domain you own, so no other app can use your links. One of the requirements for Android App Links is that you verify ownership of your domain through one of our website association methods.
Seamless user experience: Since Android App Links use a single HTTP URL for the same content on your website and in your app, users who don’t have the app installed simply go to your website instead of the app — no 404s, no errors.
Android Instant Apps support: With Android Instant Apps, your users can run your Android app without installing it. To add Instant App support to your Android app, set up Android App Links and visit g.co/InstantApps.
Engage users from Google Search: Users directly open specific content in your app by clicking a URL from Google in a mobile browser, in the Google Search app, in screen search on Android, or through Google Assistant