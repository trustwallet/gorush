---
category: patterns
subcategory: brand
confidence: low
documentType: how-to
scope: org
contentHash: 1960df5d3849
tags: [messaging]
source: README.md
verified: 2026-07-16
---

## Android Example

Send normal notification.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 2,
      "message": "Hello World Android!",
      "title": "You got message"
    }
  ]
}
```

Add `notification` payload.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 2,
      "message": "Hello World Android!",
      "title": "You got message",
      "notification" : {
        "icon": "myicon",
        "color": "#112244"
      }
    }
  ]
}
```

Add other fields which user defined via `data` field.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 2,
      "message": "Hello World Android!",
      "title": "You got message",
      "data": {
       "Nick" : "Mario",
       "body" : "great match!",
       "Room" : "PortugalVSDenmark"
      }
    }
  ]
}
```

Send messages to topics

```json
{
  "notifications": [
    {
      "to": "/topics/foo-bar",
      "platform": 2,
      "message": "This is a Firebase Cloud Messaging Topic Message"
    }
  ]
}
```

## See Also
- [ios example](../../security/ios-example.md) <!-- rel:strong -->
- [request body](../../architecture/request-body.md) <!-- rel:strong -->
- [send huawei hms notification](../../security/secrets/send-huawei-hms-notification.md) <!-- rel:related -->
- [features](../../observability/alerting/features.md) <!-- rel:weak -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:weak -->
