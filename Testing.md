

### src/test and src/androidTest

#### Local unit tests
Located at `module-name/src/test/java/`.

These are tests that run on your machine's local Java Virtual Machine (JVM). Use these tests to minimize execution time when your tests have no Android framework dependencies or when you can mock the Android framework dependencies.

At runtime, these tests are executed against a modified version of android.jar where all final modifiers have been stripped off. This lets you use popular mocking libraries, like Mockito or Roboelectric.

#### Instrumented unit tests

An Unit Android Test is a test that needs an Android device or emulator but it's different from a UI test because it doesn't start any activities.

Note that the unit test is placed in `/androidTest/` instead of `/test/`.

You should create instrumented unit tests if your tests need access to instrumentation information (such as the target app's `Context`) or if they require the real implementation of an Android framework component (such as a `Parcelable` or `SharedPreferences object`).


#### Instrumented/Integration tests
Located at `module-name/src/androidTest/java/`.

These are tests that run on a hardware device or emulator. These tests have access to Instrumentation APIs, give you access to information such as the Context of the app you are testing, and let you control the app under test from your test code. Use these tests when writing integration and functional UI tests to automate user interaction, or when your tests have Android dependencies that mock objects cannot satisfy.

### Android JUnit Rules

Android Test includes a set of JUnit rules to be used with the AndroidJUnitRunner. JUnit rules provide more flexibility and reduce the boilerplate code required in tests.

`TestCase` objects like `ActivityInstrumentationTestCase2` and `ServiceTestCase` are deprecated in favor of `ActivityTestRule` or `ServiceTestRule`.

#### ActivityTestRule (for setting up Activities)

This rule provides functional testing of a single activity. The activity under test will be launched before each test annotated with `@Test` and before any method annotated with `@Before`. It will be terminated after the test is completed and all methods annotated with `@After` are finished. The activity under test can be accessed during your test by calling `ActivityTestRule.getActivity()`.

e.g. usage
```Java
@RunWith(AndroidJUnit4.class)
@LargeTest
public class MyClassTest {
    @Rule
    public ActivityTestRule<MyClass> mActivityRule =
            new ActivityTestRule(MyClass.class);

    @Test
    public void myClassMethod_ReturnsTrue() { ... }
}
```

#### ServiceTestRule

This rule provides a simplified mechanism to start up and shut down your service before and after the duration of your test. It also guarantees that the service is successfully connected when starting a service or binding to one. The service can be started or bound using one of the helper methods. It will automatically be stopped or unbound after the test completes and any methods annotated with `@After` are finished.

### App APK and Test APK

There are two apks installed during testing,
1. App under test (our shipped apk)
2. Test apk. (apk that contains our test code)

### Test suites and test cases.

A Test case is a single peice of test class, where as a test-suite consists of collection of test cases, which can be organized in many ways.

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

### Small, Medium, Large Tests

* `Small`: this test doesn't interact with any file system or network.
* `Medium`: Accesses file systems on box which is running tests.
* `Large`: Accesses external file systems, networks, etc.

Per the Android Developers blog, a small test should take < 100ms, a medium test < 2s, and a large test < 120s.



