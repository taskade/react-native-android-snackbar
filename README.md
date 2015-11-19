# Snackbar for React Native in Android

Expose the [Snackbar android widget](http://developer.android.com/reference/android/support/design/widget/Snackbar.html) for react-native apps.

![Snackbar demo](/Example/snackbar.gif?raw=true)

Snackbar provides a lightweight feedback to users about an operation, such as saving a form or deleting a message. They are similar to Toasts, but are a bit more prominent and customizable.

Fore more info please refer to the [Google design spec on Snackbars](https://www.google.com/design/spec/components/snackbars-toasts.html#).


## Usage

Require it:

```js
var Snackbar = require('react-native-android-snackbar');
```

Then call:

```
SnackbarAndroid.show('Hello World!', options);
```

Available options:

- `duration`: one of: `Snackbar.SHORT`, `Snackbar.LONG` or `Snackbar.UNTIL_CLICK`
- `actionLabel`: text to show at the right of the snackbar
- `actionColor`: color of the action text in the snackbar. Like `red` or `#FFCA00`
- `actionCallback`: function to be evoked after the user clicks the snackbar. Keep in mind the snackbar will automatically close just before this function call


[Check full example](Example/index.android.js).


## Setup

1. Include this module in `android/settings.gradle`:
  
  ```
  include ':react-native-android-snackbar'
  include ':app'

  project(':react-native-android-snackbar').projectDir = new File(rootProject.projectDir,
    '../node_modules/react-native-android-snackbar/android')
  ```
2. Add a dependency to your app build in `android/app/build.gradle`:
  
  ```
  dependencies {
      ...
      compile project(':react-native-android-snackbar')
  }
  ```
3. Change your main activity to add a new package, in `android/app/src/main/.../MainActivity.java`:
  
  ```java
  import com.lugg.ReactSnackbar.ReactSnackbarPackage; // Add new import

  public class MainActivity extends Activity implements DefaultHardwareBackBtnHandler {

      private ReactInstanceManager mReactInstanceManager;
      private ReactRootView mReactRootView;

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          mReactRootView = new ReactRootView(this);

          mReactInstanceManager = ReactInstanceManager.builder()
                  .setApplication(getApplication())
                  .setBundleAssetName("index.android.bundle")
                  .setJSMainModuleName("index.android")
                  .addPackage(new MainReactPackage())
                  .addPackage(new ReactSnackbarPackage(mReactRootView)) // add the package here
                  .setUseDeveloperSupport(BuildConfig.DEBUG)
                  .setInitialLifecycleState(LifecycleState.RESUMED)
                  .build();
  ```

