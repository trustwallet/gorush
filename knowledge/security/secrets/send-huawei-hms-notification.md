---
category: security
subcategory: secrets
confidence: low
documentType: explanation
scope: org
contentHash: 3441ff83be76
tags: [secret]
source: README.md
verified: 2026-07-22
---

## Send Huawei (HMS) notification

Send single notification with the following command.

```bash
gorush -huawei -title "Gorush with HMS" -m "your message" -hk "API Key" -hid "App ID" -t "Device token"
```

Send messages to topics.

```bash
gorush --huawei --topic "foo-bar" \
  -title "Gorush with HMS" \
  -m "This is a Huawei Mobile Services Topic Message" \
  -hk "API Key" \
  -hid "App ID"
```

- `-m`: Notification message.
- `-hk`: [Huawei Mobile Services](https://developer.huawei.com/consumer/en/doc/development/HMS-Guides/Preparations) api secret key
- `-t`: Device token.
- `--title`: Notification title.
- `--topic`: Send messages to topics. note: don't add device token.
- `--proxy`: Set `http`, `https` or `socks5` proxy url.

## See Also
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:strong -->
- [send ios notification](../../ci/workflows/send-ios-notification.md) <!-- rel:related -->
- [huawei notification](../../references/huawei-notification.md) <!-- rel:related -->
- [request body](../../architecture/request-body.md) <!-- rel:related -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
