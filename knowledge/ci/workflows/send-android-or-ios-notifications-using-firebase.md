---
category: ci
subcategory: workflows
confidence: low
documentType: how-to
scope: org
contentHash: 00c1f7029a89
tags: [command]
source: README.md
verified: 2026-07-16
---

## Send Android or iOS notifications using Firebase

Send single notification with the following command:

```bash
gorush -android -m "your message" -k "API key" -t "Device token"
```

## See Also
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:strong -->
- [request body](../../architecture/request-body.md) <!-- rel:strong -->
- [send huawei hms notification](../../security/secrets/send-huawei-hms-notification.md) <!-- rel:related -->
- [android notification payload](../../patterns/brand/voice/android-notification-payload.md) <!-- rel:related -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
