
### What is Instance ID?


Unique Id per installation of your app. also known as InstanceId or iid, usually obtained via `getID()` method.

The Instance ID service automatically issues an InstanceID when your app comes online.

THis service also has API to generate token via `getToken()`.
 All tokens issued to your app belong to the app's InstanceID.

Tokens are unique and secure, but your app or the Instance ID service may need to refresh tokens in the event of a security issue or when a user uninstalls and reinstalls your app during device restoration. Your app must implement a listener to respond to token refresh requests from the Instance ID service.
