

### Message types

1. Notification messages, also known as display messages. Will have a `notification` field, and an optional `data` field.
2. Data messages: kind of data pushed that is handled by client app. Only contains `data` field.

### Handling Messages

Extend the `FirebaseMessagingService`. with an intent filter of
`com.google.firebase.MESSAGING_EVENT`.


| App State | Notification | Data | Both |
| ---- | ---- | ---- | ---- |
| Foreground | `onMessageReceived` | `onMessageReceived` | `onMessageReceived` |
| Background | System tray | `onMessageReceived` | Notification in sys tray and data in intent extras |


General template for handling in onMessageReceived:
```java
@Override
public void onMessageReceived(RemoteMessage remoteMessage) {
    // ...

    // TODO(developer): Handle FCM messages here.
    // Not getting messages here? See why this may be: https://goo.gl/39bRNJ
    Log.d(TAG, "From: " + remoteMessage.getFrom());

    // Check if message contains a data payload.
    if (remoteMessage.getData().size() > 0) {
        Log.d(TAG, "Message data payload: " + remoteMessage.getData());

        if (/* Check if data needs to be processed by long running job */ true) {
            // For long-running tasks (10 seconds or more) use Firebase Job Dispatcher.
            scheduleJob();
        } else {
            // Handle message within 10 seconds
            handleNow();
        }

    }

    // Check if message contains a notification payload.
    if (remoteMessage.getNotification() != null) {
        Log.d(TAG, "Message Notification Body: " + remoteMessage.getNotification().getBody());
    }

    // Also if you intend on generating your own notifications as a result of a received FCM
    // message, here is where that should be initiated. See sendNotification method below.
}
```

### Sending messages

#### Sending to a specific device

To send a message to a specific device, you need to know that device's registration token.

#### Sending messages to a topic

#### Sending messages to multiple devices

#### Sending messages to device groups