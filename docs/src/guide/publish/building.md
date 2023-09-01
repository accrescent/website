# Building

Although Accrescent accepts app submissions directly from developers, the
process for building and signing an app is slightly different than what most
developers are used to. Namely, Accrescent _does not_ accept monolithic APKs.
Read this section carefully to learn how to build apps in a format the
Accrescent Developer Console will accept.

## Setup

You need to install [`bundletool`] to build apps for Accrescent. `bundletool` is
the open-source tool Google uses to generate split APKs from app bundles in the
Play Store. Rather than signing split APKs from app bundles itself, Accrescent
accepts split APKs generated and signed by developers.

There are two primary ways to use `bundletool`. The first (and easiest) way is
using the `bundletool` Gradle plugin. The second is using the `bundletool` CLI.
Both methods are covered in the following sections.

### Bundletool Gradle plugin

#### Installation

Note: This plugin is only compatible with Android Gradle Plugin 7.4.0+.

Apply the [`bundletool` Gradle plugin] to your app as described in [the plugin's
home page]. Then specify a signing configuration in your app-level build script
as follows:

```kotlin
bundletool {
    signingConfig {
        storeFile = file("keystore.jks")
        storePassword = "password"
        keyAlias = "release"
        keyPassword = "12345"
    }
}
```

Notice the similarity to [how signing configs are specified] for your app.

#### Building

You can now build split APKs for your app by running `./gradlew
buildApks${variant}`. For example, if your app has a `release` variant, you can
build the corresponding split APKs with the following command:

```
$ ./gradlew buildApksRelease
```

The resulting APK set will be generated as
`app/build/outputs/apkset/${variant}/app-${variant}.apks`.

### Bundletool CLI

#### Installation

`bundletool` can be installed from its [GitHub releases]. There's also an AUR
package for Arch Linux users.

#### Building

There are two steps to building an app for Accrescent with the bundletool CLI:

1. Building the app bundle
2. Generating split APKs from the app bundle

See [Google's documentation] for how to build an app bundle (note: signing the
bundle with an upload key is not necessary since the split APKs are signed later
and are what is actually uploaded to Accrescent).

To build an APK set (set of split APKs) from `bundletool`, see [`bundletool`'s
documentation]. Be sure to provide a non-debug keystore to the `build-apks`
command. The resulting APK set (`.apks` file) is what you will upload to the
developer console.

[`bundletool`]: https://developer.android.com/studio/command-line/bundletool
[`bundletool`'s documentation]: https://developer.android.com/studio/command-line/bundletool#generate_apks
[`bundletool` Gradle plugin]: https://github.com/accrescent/bundletool-gradle-plugin
[GitHub releases]: https://github.com/google/bundletool/releases
[Google's documentation]: https://medium.com/androiddevelopers/building-your-first-app-bundle-bbcd228bf631
[how signing configs are specified]: https://developer.android.com/studio/publish/app-signing#secure-shared-keystore
[the plugin's home page]: https://plugins.gradle.org/plugin/app.accrescent.tools.bundletool
