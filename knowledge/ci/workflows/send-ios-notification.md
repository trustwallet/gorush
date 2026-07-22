---
category: ci
subcategory: workflows
confidence: low
documentType: how-to
scope: org
contentHash: f9c414add20d
tags: [command]
source: README.md
verified: 2026-07-22
---

## Send iOS notification

Send single notification with the following command.

```bash
$ gorush -ios -m "your message" -i "your certificate path" \
  -t "device token" --topic "apns topic"
```

- `-m`: Notification message.
- `-i`: Apple Push Notification Certificate path (`pem` or `p12` file).
- `-t`: Device token.
- `--title`: Notification title.
- `--topic`: The topic of the remote notification.
- `--password`: The certificate password.

The default endpoint is APNs development. Please add `-production` flag for APNs production push endpoint.

```bash
$ gorush -ios -m "your message" -i "your certificate path" \
  -t "device token" \
  -production
```

## See Also
- [send huawei hms notification](../../security/secrets/send-huawei-hms-notification.md) <!-- rel:strong -->
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
- [request body](../../architecture/request-body.md) <!-- rel:related -->
- [ios alert payload](../../build/ios-alert-payload.md) <!-- rel:related -->
