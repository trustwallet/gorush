---
category: patterns
subcategory: brand/voice
confidence: low
documentType: how-to
scope: org
contentHash: f5eb4bf3db10
tags: [messaging]
source: README.md
verified: 2026-07-22
---

## Android notification payload

| name           | type   | description                                                                                               | required | note |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|----------|------|
| icon           | string | Indicates notification icon.                                                                              | -        |      |
| tag            | string | Indicates whether each notification message results in a new entry on the notification center on Android. | -        |      |
| color          | string | Indicates color of the icon, expressed in #rrggbb format                                                  | -        |      |
| click_action   | string | The action associated with a user click on the notification.                                              | -        |      |
| body_loc_key   | string | Indicates the key to the body string for localization.                                                    | -        |      |
| body_loc_args  | string | Indicates the string value to replace format specifiers in body string for localization.                  | -        |      |
| title_loc_key  | string | Indicates the key to the title string for localization.                                                   | -        |      |
| title_loc_args | string | Indicates the string value to replace format specifiers in title string for localization.                 | -        |      |

See more detail about [Firebase Cloud Messaging HTTP Protocol reference](https://firebase.google.com/docs/cloud-messaging/http-server-ref#send-downstream).

## See Also
- [ios alert payload](../../../build/ios-alert-payload.md) <!-- rel:strong -->
- [request body](../../../architecture/request-body.md) <!-- rel:strong -->
- [features](../../../observability/alerting/features.md) <!-- rel:related -->
- [ios example](../../../security/ios-example.md) <!-- rel:related -->
- [send huawei hms notification](../../../security/secrets/send-huawei-hms-notification.md) <!-- rel:related -->
