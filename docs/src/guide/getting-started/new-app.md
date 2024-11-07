# Submitting a new app

## Creating an account

To submit an app to Accrescent, you first need to create an account on the [developer console].
Currently login with GitHub is the only supported login method.

Sign-up is not yet available to the general public and is only permitted for allowlisted GitHub
accounts. This choice was made to ensure that all developers on Accrescent are willing to tolerate
the lackluster user experience, console bugs, and frequent policy changes resultant of Accrescent
being in its early stages. If you are not allowlisted and are still interested in publishing on
Accrescent, you may contact us at <contact@accrescent.app> to request being allowlisted.

## Submission process

To upload a new app, click the "New app" button on your dashboard. You will be
presented with an upload form. Upload the APK set (`.apks` file) you generated
earlier as well as an app icon. The APK set must be less or equal to 150 MiB in
size and the icon must be a 512 x 512 PNG. If you already have a Play Store
icon, you can use it here. If you don't have an icon, you can [generate one in
Android Studio] (make sure "Play Store icon" is selected).

Click "Upload" after you've selected the correct files. Once your files are
finished uploading, you'll be presented with an autofilled form with basic
information about your app. You may edit the display name if you wish. This is
the name that will appear to users in the store. Once you're satisfied that your
app's information is correct, click "Submit" to begin the review process.

If some or all of your app's functionality requires authentication to access,
please provide test account credentials for the review process. This is
currently not possible within the developer console, so you will need to contact
the Accrescent team directly to provide them.

## After you submit

A reviewer will be assigned to your app after you submit it. To increase its
chances of being accepted, please review the [app requirements] later in this
guide before submitting.

If the app is accepted, it will be passed on to have its metadata
cryptographically signed into the store. This process ensures Accrescent's
security even if one of its servers is compromised. You don't need to do
anything at this point. Once your app is published, you will be notified and it
will show up under "My apps" in the developer console

[app requirements]: ../appendix/requirements.md
[developer console]: https://console.accrescent.app
[generate one in Android Studio]: https://developer.android.com/studio/write/image-asset-studio#create-adaptive
