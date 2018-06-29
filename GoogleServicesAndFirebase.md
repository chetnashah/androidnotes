
### google-services.json file

1. `project_info` field: contains general information about your project.

2. `client` field: Array that contains information about the clients(Android apps) that you have added to the project.

When processing the JSON file for your Android app, the plugin only uses the client object that matches your package name (for the current build type) based on the following logic:

For each member of the client array:
Check the value of  `client_info/android_client_info/package_name`
If the package name matches this value, return the member object.
If none of the members of client match the package name, an exception is thrown.


### gradle plugin 'com.google.gms:google-services'

The google-services plugin has two main functions:

1. Process the `google-services.json` file and produce Android resources that can be used in your application's code. See Adding the JSON File more information.
2. Add dependencies for basic libraries required for the services you have enabled. This step requires that the `apply plugin: 'com.google.gms.google-services'` line be at the bottom of your app/build.gradle file so that no dependency collisions are introduced. You can see the result of this step by running ./gradlew :app:dependencies.

The `google-services.json` is generally placed in `app/` directory.

**Note** : see where to place `google-services.json` for services specific to product flavors.

## Meteor vs Firebase

1. Firebase and Meteor
    * data loading
    * security
    * accounts system
    * reactivity
    * hosting platform
2. Firebase only
    * built-in crash reporting, analytics, etc
    * backend as a service
    * data explorer
    * just read and write data
3. Meteor only
    * open source
    * reads from your existing database, so you own your data
    * build system for JavaScript
    * mobile builds
    * ability to write backend code

## FireBase

FireBase is essentially a backend as a service, providing features like data synchronization etc. also.

### FireBase RealTime DAtabase

Realtime Database is Firebase's original database. It's an efficient, low-latency solution for mobile apps that require synced states across clients in realtime

### Firebase Cloud FireStore

Cloud Firestore is Firebase's new flagship database for mobile app development. It improves on the successes of the Realtime Database with a new, more intuitive data model. Cloud Firestore also features richer, faster queries and scales better than the Realtime Database

### Firebase RealtimeDatabse vs FireStore

https://firebase.google.com/docs/database/rtdb-vs-firestore?authuser=0

### Firebase Remote Config

It is a config (key-value) data that lives in the cloud, and which our app can read easily for various use cases.
Used for A/B testing.
Firebase Remote Config is a cloud service that lets you change the behavior and appearance of your app without requiring users to download an app update. When using Remote Config, you create in-app default values that control the behavior and appearance of your app. Then, you can later use the Firebase console or the Remote Config REST API to override in-app default values for all app users or for segments of your user base. Your app controls when updates are applied, and it can frequently check for updates and apply them with a negligible impact on performance


### Firebase Dynamic links

Configurable and more powerful than regular deep links. (contrast with app links).

Firebase Dynamic Links are links that work the way you want, on multiple platforms, and whether or not your app is already installed.


With Dynamic Links, your users get the best available experience for the platform they open your link on. If a user opens a Dynamic Link on iOS or Android, they can be taken directly to the linked content in your native app. If a user opens the same Dynamic Link in a desktop browser, they can be taken to the equivalent content on your website.

In addition, Dynamic Links work across app installs: if a user opens a Dynamic Link on iOS or Android and doesn't have your app installed, the user can be prompted to install it; then, after installation, your app starts and can access the link.

### Firebase App indexing

#### App links vs Deep links

When using deep links, you may see a disambiguation dialog, 
e.g. you have deeplink for `https://myawesomeapp.com/somecontent`.
Disambiguation dialog shows your app as well as browser as potential handlers for this deep link.

With `app links`, you register ownership of links, which help you prevent you disambiguation dialog and lead you straight to the app.
It is a two step process
1. add deep links for the domain links
2. verify domain with google and hence convert them to app links.

In order to associate your app with your site, we will need a `assetlinks.json` file.

Kind of used with app links. Great way to boost your business and
improve discoverability. A great way to funnel search traffic back into app.

Firebase App Indexing gets your app into Google Search. If users have your app installed, they can launch your app and go directly to the content they're searching for. App Indexing reengages your app users by helping them find both public and personal content right on their device, even offering query autocompletions to help them more quickly find what they need. If users don’t yet have your app, relevant queries trigger an install card for your app in Search results.

Use cases:
1. **Search results** 
2. **Installs** - show install button along with search result.
3. **Autocompletions** - User can see app content
4. **Assistant**
5. **Ad targeting**



### Firebase on Android Client

#### Firebase events
https://www.youtube.com/watch?v=dBscwaqNPuk

On any data change inside realtimedatabase, firebase emits two kinds of events:
1. value events. (full data snapshot)

Usefu for primitive data changes. Snapshot value is full data at given path of databasereference.

2. child events (`child_added`, `child_changed`, `child_removed`)

Useful when someone adds/updates/removes an item in a list i.e (object of key-value pairs).
Snapshot value for child events is usually the item i.e. (key-value pair)

In android/java, they are captured via `ValueEventListener` and `ChildListener` respectively on a `DatabaseReference`.

#### Firebase Query class

The `Query` class (and its subclass, DatabaseReference) are used for reading data. Listeners (known as `ChildListener`) are attached, and they will be triggered when the corresponding data changes.

Instances of Query are obtained by calling `startAt()`, `endAt()`, or `limit()` on a `DatabaseReference`.

#### Reading and writing data to firebase using `DatabaseReference`

All Firebase Realtime Database data is stored as JSON objects. You can think of the database as a cloud-hosted JSON tree

1. get a reference i.e 
```java
// Write a message to the database
FirebaseDatabase database = FirebaseDatabase.getInstance();
DatabaseReference myRef = database.getReference("message");
```

2. Working with lists

`push` method is available on a `DatabaseReference`, and calling `push()` returns a DatabaseReference to newly added item.

Use the `push()` method to append data to a list in multiuser applications. The `push()` method generates a unique key every time a new child is added to the specified Firebase reference. By using these auto-generated keys for each new element in the list, several clients can add children to the same location at the same time without write conflicts. The unique key generated by `push()` is based on a timestamp, so list items are automatically ordered chronologically.

You can use the reference to the new data returned by the `push()` method to get the value of the child's auto-generated key or set data for the child. Calling `getKey()` on a push() reference returns the value of the auto-generated key.

##### ValueEventListener vs ChildEventListener to observe data values

They do almost same thing, though `ChildEventListener` can be sometimes more flexible: with `ChildEventListener` you can specify different behavior for 4 actions (`onChildAdded`, `onChildChanged`, `onChildMoved` and `onChildRemoved`), while `ValueEventListener` provides only  `onDataChanged`.

Also `ChildEventListener` provides DataSnapshots (immutable copies of the data) at child's location while `ValueEventListener` provides a DataSnapshot of a whole node.




#### Firebase Recycler Adapter

https://github.com/firebase/FirebaseUI-Android/blob/master/database/README.md

If you're displaying a list of data, you likely want to bind the Chat objects to a RecyclerView. This means implementing a custom RecyclerView.Adapter and coordinating updates with the ChildEventListener.

Fear not, FirebaseUI does all of this for you automatically!

Using the FirebaseRecyclerAdapter
The FirebaseRecyclerAdapter binds a Query to a RecyclerView. When data is added, removed, or changed these updates are automatically applied to your UI in real time.


#### Firebase Storage : FirebaseStorageReference for file storage and Google Cloud Storage

Helps you Store and retrieve user-generated files like images, audio, and video without server-side code

https://firebase.google.com/docs/storage/android/upload-files

Your files are stored in a Google Cloud Storage bucket. The files in this bucket are presented in a hierarchical structure, just like the file system on your local hard disk, or the data in the Firebase Realtime Database. By creating a reference to a file, your app gains access to it. These references can then be used to upload or download data, get or update metadata or delete the file. **A reference can either point to a specific file or to a higher level node in the hierarchy.**

If you've used the Firebase Realtime Database, these paths should seem very familiar to you. However, your file data is stored in Google Cloud Storage, not in the Realtime Database.

```java
// Create a storage reference from our app
StorageReference storageRef = storage.getReference();

// Child references can also take paths
// spaceRef now points to "images/space.jpg
// imagesRef still points to "images"
StorageReference spaceRef = storageRef.child("images/space.jpg");

// Reference's path is: "images/space.jpg"
// This is analogous to a file path on disk
spaceRef.getPath();

// Reference's name is the last segment of the full path: "space.jpg"
// This is analogous to the file name
spaceRef.getName();

// Reference's bucket is the name of the storage bucket that the files are stored in
spaceRef.getBucket();
```

**Uploading Files**

`StorageMetaData` is a class to add custom metadata to a particular file.

1. setup filename via `Storage.getReference(path)`.
2. create storage metadata via `StorageMetaData.builder`. 
3. Get async task result for upload task 
```java
UploadTask task = fileRef.putBytes(data, metaData)
```

Or use putFile
```java
Uri file = Uri.fromFile(new File("path/to/images/rivers.jpg"));
StorageReference riversRef = storageRef.child("images/"+file.getLastPathSegment());
uploadTask = riversRef.putFile(file);
```



