# App updates

## Submission process

To update one of your existing apps, go to "My apps" in the developer console
and click "Upload new update" under the app you want to update. You'll be
presented with a similar form to the new app form. Select an APK set that
represents your app update and it will be automatically uploaded and checked.
You'll be shown the info Accrescent could gather about your update. If you're
satisfied, click "Submit."

Different things may happen with your update after you submit it depending on
its content. The specific process is explained below.

## Review process

Accrescent's update process is unique in that most of the time, developers don't
need to wait to have their updates reviewed. Instead they are published
immediately after the developer submits them. This approach may sound like a bad
idea at first, but it has several advantages:

- security updates can be published immediately after they're ready
- updates can (theoretically) be fully automated through CD pipelines
- developers have fewer frustrating review experiences
- Accrescent developers spend less time reviewing and more time developing

To mitigate the potential for a malicious or compromised developer to abuse this
process, all updates requesting new sensitive permissions (as determined by the
developer console) will require manual review.

For example, say an app was approved requesting the `READ_SMS` permission. The
developer uploads an update that requests the `READ_SMS` and
`MANAGE_EXTERNAL_STORAGE` permissions. Because `MANAGE_EXTERNAL_STORAGE` is
newly requested and Accrescent considers it to be a sensitive permission, that
update will require manual review.

Continuing the example, let's say that update is approved and the developer
uploads anoter update requesting the `READ_SMS` and `MANAGE_EXTERNAL_STORAGE`
permissions. Since the app was previously approved to request both of these
permissions, the second update will not require manual review and will instead
be published immediately after the developer submits it.
