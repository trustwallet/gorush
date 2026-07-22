---
category: code-conventions
subcategory: git
confidence: low
documentType: tutorial
scope: org
contentHash: 28f6ef85ae06
tags: [version]
source: README.md
verified: 2026-07-22
---

## GET /api/stat/app

Show success or failure counts information of notification.

```json
{
  "version": "v1.6.2",
  "queue_max": 8192,
  "queue_usage": 0,
  "total_count": 77,
  "ios": {
    "push_success": 19,
    "push_error": 38
  },
  "android": {
    "push_success": 10,
    "push_error": 10
  },
  "huawei": {
    "push_success": 3,
    "push_error": 1
  }
}
```

## See Also
- [get metrics](../../observability/metrics/get-metrics.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:strong -->
- [android example](../../patterns/brand/android-example.md) <!-- rel:related -->
- [send ios notification](../../ci/workflows/send-ios-notification.md) <!-- rel:related -->
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:related -->
