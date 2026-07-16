---
category: security
confidence: low
documentType: explanation
scope: org
contentHash: b41155a0dcd6
tags: [sandbox]
source: README.md
verified: 2026-07-16
---

## iOS Example

Send normal notification.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 1,
      "message": "Hello World iOS!"
    }
  ]
}
```

The following payload asks the system to display an alert with a Close button and a single action button.The title and body keys provide the contents of the alert. The “PLAY” string is used to retrieve a localized string from the appropriate Localizable.strings file of the app. The resulting string is used by the alert as the title of an action button. This payload also asks the system to badge the app’s icon with the number 5.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 1,
      "badge": 5,
      "alert": {
        "title" : "Game Request",
        "body" : "Bob wants to play poker",
        "action-loc-key" : "PLAY"
      }
    }
  ]
}
```

The following payload specifies that the device should display an alert message, plays a sound, and badges the app’s icon.

```json
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 1,
      "message": "You got your emails.",
      "badge": 9,
      "sound": {
        "critical": 1,
        "name": "default",
        "volume": 1.0
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
      "platform": 1,
      "message": "Hello World iOS!",
      "data": {
        "key1": "welcome",
        "key2": 2
      }
    }
  ]
}
```

Support send notification from different environment. See the detail of [issue](https://github.com/appleboy/gorush/issues/246).

```diff
{
  "notifications": [
    {
      "tokens": ["token_a", "token_b"],
      "platform": 1,
+     "production": true,
      "message": "Hello World iOS Production!"
    },
    {
      "tokens": ["token_a", "token_b"],
      "platform": 1,
+     "development": true,
      "message": "Hello World iOS Sandbox!"
    }
  ]
}
```

## See Also
- [ios alert payload](../build/ios-alert-payload.md) <!-- rel:strong -->
- [request body](../architecture/request-body.md) <!-- rel:strong -->
- [android example](../patterns/brand/android-example.md) <!-- rel:strong -->
- [android notification payload](../patterns/brand/voice/android-notification-payload.md) <!-- rel:related -->
- [run grpc service](../tests/run-grpc-service.md) <!-- rel:related -->
