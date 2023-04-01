# Building

Although Accroissant accepts app submissions directly from developers, the
process for building and signing an app is slightly different than what most
developers are used to. Namely, Accroissant _does not_ accept monolithic APKs.
Read this section carefully to learn how to build apps in a format the
Accroissant Developer Console will accept.

## Setup

You need to install [`bundletool`] to build apps for Accroissant. `bundletool` is
the open-source tool Google uses to generate split APKs from app bundles in the
Play Store. Rather than signing split APKs from app bundles itself, Accroissant
accepts split APKs generated and signed by developers.

`bundletool` can be installed from its [GitHub releases]. There's also an AUR
package for Arch Linux users.

## Building

There are two steps to building an app for Accroissant:

1. Building the app bundle
2. Generating split APKs from the app bundle

See [Google's documentation] for how to build an app bundle (note: signing the
bundle with an upload key is not necessary since the split APKs are signed later
and are what is actually uploaded to Accroissant).

To build an APK set (set of split APKs) from `bundletool`, see [`bundletool's
documentation`]. Be sure to provide a non-debug keystore to the `build-apks`
command. The resulting APK set (`.apks` file) is what you will upload to the
developer console.

[`bundletool`]: https://developer.android.com/studio/command-line/bundletool
[`bundletool's documentation`]: https://developer.android.com/studio/command-line/bundletool#generate_apks
[GitHub releases]: https://github.com/google/bundletool/releases
[Google's documentation]: https://medium.com/androiddevelopers/building-your-first-app-bundle-bbcd228bf631
