

### src/test and src/androidTest

Local unit tests (`/src/test/java/`)
Unit tests that run locally on the Java Virtual Machine (JVM). Use these tests to minimize execution time when your tests have no Android framework dependencies or when you can mock the Android framework dependencies.

Instrumented tests (`/src/androidTest/java/`)
Unit tests that run on an Android device or emulator. These tests have access to Instrumentation information, such as the Context of the app you are testing. Use these tests when your tests have Android dependencies that mock objects cannot satisfy.

### Build types, build flavors and build variants

**Build Types**
Build types define certain properties that Gradle uses when building and packaging your app, and are typically configured for different stages of your development lifecycle. For example, the debug build type enables debug options and signs the APK with the debug key, while the release build type may shrink, obfuscate, and sign your APK with a release key for distribution. You must define at least one build type in order to build your app—Android Studio creates the debug and release build types by default. To start customizing packaging settings for your app, learn how to Configure Build Types.

**Product Flavors**
Product flavors represent different versions of your app that you may release to users, such as free and paid versions of your app. You can customize product flavors to use different code and resources, while sharing and reusing the parts that are common to all versions of your app. Product flavors are optional and you must create them manually. To start creating different versions of your app, learn how to Configure Product Flavors.
Build Variants

A **build variant** is a cross product of a build type and product flavor, and is the configuration Gradle uses to build your app. Using build variants, you can build the debug version of your product flavors during development, or signed release versions of your product flavors for distribution. Although you do not configure build variants directly, you do configure the build types and product flavors that form them. Creating additional build types or product flavors also creates additional build variants. To learn how to create and manage build variants, read the Configure Build Variants overview

`src/productFlavorBuildType/`
e.g. `src/freeDebug`, `src/paidRelease`
Create this source set to include code and resources only for a specific build variant.

`src/main/`
This source set includes code and resources common to all build variants.

`src/buildType/`
e.g. `src/debug` and `src/release`
Create this source set to include code and resources only for a specific build type.

`src/productFlavor/`
e.g. `src/paid`, `src/mock`, `src/free`
Create this source set to include code and resources only for a specific product flavor.

source folders for tests with flavors:
`src/testproductFlavor` and `src/androidTestProductFlavor`
e.g. `src/testPaid`, `src/androidTestPaid` etc.

###

Just like android combines `src/main` with `src/flavor` for a specific build flavor,
For testing, android will combine `src/test` with `src/testFlavor`

### Source-Sets and product flavors