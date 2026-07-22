---
title: "Notification Dispatch: routerEngine and SendNotification"
category: architecture
tags: [push, dispatch, apns, fcm, hms, platform-routing]
confidence: high
source: notify/notification.go, notify/notification_apns.go, notify/notification_fcm.go, notify/notification_hms.go, router/server.go
updated: 2026-07-22
---

# Notification Dispatch: routerEngine and SendNotification

## routerEngine — the HTTP wiring hub

`routerEngine` in `router/server.go` is the single function that assembles the entire Gin HTTP router: it configures zerolog level, registers Prometheus metrics once via `sync.Once`, sets gin mode, attaches all middleware (logger, recovery, version header, stats), and registers all API routes. It is called from `RunHTTPServer` and `RunAutoTLSServer`. Every new API endpoint must be added here.

**Why it's central (fan-in 3, fan-out 6):** Three separate server-start paths call it (normal HTTP, TLS, Lambda), and it wires 6+ handlers, so all HTTP surface changes go through this one function.

## PushNotification model

The `PushNotification` struct is the unified notification envelope. Key discriminator:

```go
Platform int // 1 = iOS (APNs), 2 = Android (FCM), 3 = Huawei (HMS)
```

iOS-specific fields: `Topic`, `PushType`, `Badge`, `Alert` (struct), `Expiration`, `ApnsID`, `CollapseID`, `Category`, `ThreadID`, `URLArgs`, `Production`, `Development`, `Apns` (raw headers dict).

Android/FCM-specific fields: `APIKey`, `To`, `CollapseKey`, `DelayWhileIdle`, `TimeToLive`, `RestrictedPackageName`, `DryRun`, `Condition`, `Notification` (FCM notification struct).

Huawei/HMS-specific fields: `AppID`, `AppSecret`, `HuaweiNotification`, `HuaweiData`, `HuaweiCollapseKey`, `HuaweiTTL`, `BiTag`, `FastAppTarget`.

## SendNotification dispatch

```
SendNotification(msg QueuedMessage, cfg *ConfYaml)
    └── switch platform
          ├── 1 (iOS)    → PushToIOS
          ├── 2 (Android)→ PushToAndroid
          └── 3 (Huawei) → PushToHuawei
    └── if FeedbackURL set → DispatchFeedback (per log entry)
```

`SendNotification` is called by the `Run` closure, which is the queue worker function set via `queue.WithWorker`.

## PushToIOS (APNs)

`InitAPNSClient` initializes the APNs HTTP/2 client from config:
- `.p12` → `certificate.FromP12File`
- `.pem` → `certificate.FromPemFile`
- `.p8` → token-based auth via `token.AuthKeyFromFile` (uses KeyID + TeamID)

The `configureHTTP2ConnHealthCheck` function (fan-in 3) sets up the underlying HTTP/2 transport health check with `idleConnTimeout=90s`, `tlsDialTimeout=20s`, `tcpKeepAlive=60s`. It is called from all three APNs client init paths (p12, p8, pem), making it the most-called helper inside APNs setup.

`PushToIOS` iterates tokens, builds an `apns2.Notification` payload, sends it, and tracks success/error in `status.StatStorage`.

## PushToAndroid (FCM)

`PushToAndroid` builds an `fcm.Message`, sets registration IDs (or topic), and calls the FCM HTTP API. Up to 1000 tokens per batch. Failures are logged via `logPush` (fan-in 3 — called from success, partial-failure, and retry paths).

## PushToHuawei (HMS)

`PushToHuawei` initialises the HMS client with AppID + AppSecret, builds the HMS message, and sends. Up to 500 tokens per batch. Token limit differs from FCM (500 vs 1000).

## Feedback webhook

If `cfg.Core.FeedbackURL` is non-empty, after each `SendNotification` call the `DispatchFeedback` function in `notify/feedback.go` posts each `LogPushEntry` as JSON to that URL, with a configurable timeout (`cfg.Core.FeedbackTimeout`, default 10s). This is the async error reporting path.

## Validation

`CheckMessage` is called before enqueueing. Key constraints:
- At least one token required (unless topic message for FCM/HMS)
- FCM: max 1000 tokens, TTL ≤ 2419200s (4 weeks)
- HMS: max 500 tokens

`CheckPushConf` validates config at startup: at least one platform must be enabled, each enabled platform must have its credentials set.

## See Also
- [overview.md](overview.md)
- [queue-processing.md](queue-processing.md)
- [credential handling](../security/credential-handling.md) <!-- rel:strong -->
- [logging](../observability/logging.md) <!-- rel:strong -->
- [configuration](../libs/configuration.md) <!-- rel:strong -->
