# flutter_flavors_bug

This is a Flutter project created via `flutter create flutter_flavors_bug`.

The `android/app/build.gradle` was modified to include productFlavors with two dimensions:

```groovy
flavorDimensions "api","track"
productFlavors {
    production {
        dimension "api"
    }
    development {
        dimension "api"
    }
    internal {
        dimension "track"
    }
    external {
        dimension "track"
    }
}
```

Running `flutter run --flavor development` results in the following error:

```
$ flutter run --flavor development                                     
Using hardware rendering with device sdk gphone64 arm64. If you notice graphics artifacts, consider enabling software rendering with
"--enable-software-rendering".
Launching lib/main.dart on sdk gphone64 arm64 in debug mode...

FAILURE: Build failed with an exception.

* What went wrong:
Task 'assembleDevelopmentDebug' not found in root project 'android'.

* Try:
> Run gradlew tasks to get a list of available tasks.
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 797ms
Running Gradle task 'assembleDevelopmentDebug'...                1,287ms

┌─ Flutter Fix ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ [!]  Gradle project does not define a task suitable for the requested build.                                                          │
│                                                                                                                                       │
│ The /Users/felix/Desktop/flutter_flavors_bug/android/app/build.gradle file defines product flavors: development, developmentexternal, │
│ developmentinternal, production, productionexternal, productioninternal. You must specify a --flavor option to select one of them.    │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
Exception: Gradle task assembleDevelopmentDebug failed with exit code 1
```

The error states that the `build.gradle` file defines product flavors: `development, developmentexternal, developmentinternal, production, productionexternal, productioninternal` which is incorrect since `development` and `production` are not compatible with `flutter run` or `flutter build`.

