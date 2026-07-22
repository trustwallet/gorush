---
category: build
confidence: low
documentType: reference
scope: org
contentHash: efe8794035fb
tags: [bundle]
source: README.md
verified: 2026-07-22
---

## iOS alert payload

| name           | type             | description                                                                                      | required | note |
|----------------|------------------|--------------------------------------------------------------------------------------------------|----------|------|
| title          | string           | Apple Watch & Safari display this string as part of the notification interface.                  | -        |      |
| body           | string           | The text of the alert message.                  | -        |      |
| subtitle       | string           | Apple Watch & Safari display this string as part of the notification interface.                  | -        |      |
| action         | string           | The label of the action button. This one is required for Safari Push Notifications.              | -        |      |
| action-loc-key | string           | If a string is specified, the system displays an alert that includes the Close and View buttons. | -        |      |
| launch-image   | string           | The filename of an image file in the app bundle, with or without the filename extension.         | -        |      |
| loc-args       | array of strings | Variable string values to appear in place of the format specifiers in loc-key.                   | -        |      |
| loc-key        | string           | A key to an alert-message string in a Localizable.strings file for the current localization.     | -        |      |
| title-loc-args | array of strings | Variable string values to appear in place of the format specifiers in title-loc-key.             | -        |      |
| title-loc-key  | string           | The key to a title string in the Localizable.strings file for the current localization.          | -        |      |

See more detail about [APNs Remote Notification Payload](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/PayloadKeyReference.html).

## See Also
- [ios example](../security/ios-example.md) <!-- rel:strong -->
- [android notification payload](../patterns/brand/voice/android-notification-payload.md) <!-- rel:strong -->
- [support platform](../libs/support-platform.md) <!-- rel:strong -->
- [request body](../architecture/request-body.md) <!-- rel:strong -->
- [send ios notification](../ci/workflows/send-ios-notification.md) <!-- rel:weak -->
