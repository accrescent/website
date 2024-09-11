# Requirements

Accrescent has certain minimum requirements for all apps submitted to it to
ensure the privacy and security of its users. This page documents these
requirements for developers to reference before submitting their app so they
know how to best improve their chances for acceptance.

These requirements are not exhaustive and Accrescent reserves the right to
modify them at any time. However, the Accrescent developers attempt to make this
list as thorough as possible and give notice to developers well in advance for
major requirement updates. If you see something missing or incorrect, please
submit a pull request at this site's [GitHub repository].

## Automated checks

The following checks are run automatically on all apps before the developer
submits them. If any of them fail, an error will show in the developer console
and the app cannot be submitted.

#### Debug certificate

Apps may not be signed with a debug certificate. They are [insecure by design]
and so are not permitted in Accrescent.

#### Native code

Accrescent supports the following architectures:

- arm64
- armeabi-v7a
- x86_64
- x86

Apps containing 32-bit native code for a supported architecture must also include 64-bit native code
for the corresponding architecture. Additionally, apps containing native code must support at least
one of Accrescent's supported architectures.

For more information, see [Google's documentation on 64-bit support].

#### Target SDK

Accrescent currently follows [Google Play's target SDK requirements] with a few
major changes:

- there are no formal timeline extension requests
- Accrescent will _remove_ apps when they don't meet the target SDK requirements
  for existing apps, not just make them less discoverable

#### `android:debuggable`

The [`android:debuggable`] attribute in the Android manifest must not be "true".

#### `android:testOnly`

The [`android:testOnly`] attribute in the Android manifset must not be "true".

#### `android:usesCleartextTraffic`

The [`android:usesCleartextTraffic`] attribute in the Android manifest must not
be "true". This check may move to manual review in the future.

## Manual checks

The following are checks done by reviewers in reference to this document when
manually reviewing an app.

### Self-updaters

Apps may not have self-updaters. This includes improper use of the
`REQUEST_INSTALL_PACKAGES` permission as outlined below, downloaders which
prompt the user to update from an APK, and direct links to sources which may
encourage or confuse the user into updating from a location outside of
Accrescent.

### Sensitive permissions

Addition of any of the following permissions in an app update will trigger a
manual review and their usage will also be reviewed in new apps:

- `ACCESS_BACKGROUND_LOCATION`
- `ACCESS_COARSE_LOCATION`
- `ACCESS_FINE_LOCATION`
- `BLUETOOTH_SCAN`
- `CAMERA`
- `MANAGE_EXTERNAL_STORAGE`
- `NEARBY_WIFI_DEVICES`
- `PROCESS_OUTGOING_CALLS`
- `QUERY_ALL_PACKAGES`
- `READ_CALL_LOG`
- `READ_CONTACTS`
- `READ_EXTERNAL_STORAGE`
- `READ_MEDIA_AUDIO`
- `READ_MEDIA_IMAGES`
- `READ_MEDIA_VIDEO`
- `READ_PHONE_NUMBERS`
- `READ_PHONE_STATE`
- `READ_SMS`
- `RECEIVE_MMS`
- `RECEIVE_SMS`
- `RECEIVE_WAP_PUSH`
- `RECORD_AUDIO`
- `REQUEST_INSTALL_PACKAGES`
- `SEND_SMS`
- `WRITE_CALL_LOG`
- `WRITE_CONTACTS`
- `SYSTEM_ALERT_WINDOW`

Review will fail if an app requests a permission it does not reasonably require
to function or uses a permission to share sensitive user data without informed
consent. More specific requirements are laid out below for the following
permissions:

- `MANAGE_EXTERNAL_STORAGE`
- `REQUEST_INSTALL_PACKAGES`

#### `MANAGE_EXTERNAL_STORAGE`

The `MANAGE_EXTERNAL_STORAGE` permission may only be requested for one or more
of the following use cases:

- file management, such as for a file manager app

`MANAGE_EXTERNAL_STORAGE` is highly invasive and almost always unnecessary.
Developers should heavily consider using internal app storage, the [`MediaStore`
API], and/or the [Storage Access Framework] instead.

#### `REQUEST_INSTALL_PACKAGES`

The `REQUEST_INSTALL_PACKAGES` permission may only be requested for one or more
of the following use cases:

- web browsers
- file sharing
- messengers which support sending APKs

`REQUEST_INSTALL_PACKAGES` _may not_ be used for self-updating or updating or
installing other apps.

### Service intent filters

Adding any of the following actions to a service's intent filter will trigger a
manual review:

- `android.accessibilityservice.AccessibilityService`
- `android.net.VpnService`
- `android.view.InputMethod`

More specific requirements for the following actions are laid out below:

- `android.accessibilityservice.AccessibilityService`
- `android.net.VpnService`

#### `android.accessibilityservice.AccessibilityService`

Accessibility services are highly invasive, presenting a security and privacy
risk to users. As such, they are heavily restricted on Accrescent and may only
be used to help users with disabilities interact with the device.

#### `android.net.VpnService`

VPN services may only be used by apps that have a VPN as their core
functionality. They _must_ encrypt all data between the device and the VPN
tunnel endpoint. They _may not_ be used to collect sensitive user data without
informed consent.

[`android:debuggable`]: https://developer.android.com/guide/topics/manifest/application-element#debug
[`android:testOnly`]: https://developer.android.com/guide/topics/manifest/application-element#testOnly
[`android:usesCleartextTraffic`]: https://developer.android.com/guide/topics/manifest/application-element#usesCleartextTraffic
[GitHub repository]: https://github.com/accrescent/accrescent.app
[Google Play's target SDK requirements]: https://support.google.com/googleplay/android-developer/answer/11926878
[Google's documentation on 64-bit support]: https://developer.android.com/google/play/requirements/64-bit
[insecure by design]: https://developer.android.com/studio/publish/app-signing#debug-mode
[`MediaStore` API]: https://developer.android.com/training/data-storage/shared/media
[Storage Access Framework]: https://developer.android.com/guide/topics/providers/document-provider
