---
category: patterns
subcategory: brand/voice
confidence: medium
documentType: how-to
scope: org
contentHash: 8803714eb9c3
tags: [messaging]
source: README.md
verified: 2026-07-22
---

## Send Android notification

Send single notification with the following command.

```bash
gorush -android -m "your message" -k "API Key" -t "Device token"
```

Send messages to topics.

```bash
gorush --android --topic "/topics/foo-bar" \
  -m "This is a Firebase Cloud Messaging Topic Message" \
  -k your_api_key
```

- `-m`: Notification message.
- `-k`: [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) api key
- `-t`: Device token.
- `--title`: Notification title.
- `--topic`: Send messages to topics. note: don't add device token.
- `--proxy`: Set `http`, `https` or `socks5` proxy url.

## See Also
- [send huawei hms notification](../../../security/secrets/send-huawei-hms-notification.md) <!-- rel:strong -->
- [send ios notification](../../../ci/workflows/send-ios-notification.md) <!-- rel:related -->
- [request body](../../../architecture/request-body.md) <!-- rel:related -->
- [features](../../../observability/alerting/features.md) <!-- rel:related -->
- [send android or ios notifications using firebase](../../../ci/workflows/send-android-or-ios-notifications-using-firebase.md) <!-- rel:related -->
