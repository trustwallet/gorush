---
title: Notification Dispatch — SendNotification, PushToIOS, PushToAndroid, PushToHuawei
category: architecture
tags: [notification, apns, fcm, hms, dispatch, queue]
confidence: high
source: notify/notification.go, notify/notification_apns.go, notify/notification_fcm.go, notify/notification_hms.go
updated: 2026-07-16
---

# Notification Dispatch

The `notify/` package is the core of gorush. It handles platform dispatch, retry logic, payload construction, and result logging.

## Dispatch Entry Point: `SendNotification`

```go
func SendNotification(req queue.QueuedMessage, cfg *config.ConfYaml) (resp *ResponsePush, err error)
```

Called by the queue worker via the `Run` closure. Deserializes the message if needed, then switches on `Platform`:

| `Platform` | Constant | Target |
|---|---|---|
| 1 | `core.PlatFormIos` | `PushToIOS` (APNs) |
| 2 | `core.PlatFormAndroid` | `PushToAndroid` (FCM) |
| 3 | `core.PlatFormHuawei` | `PushToHuawei` (HMS) |

After delivery, if `cfg.Core.FeedbackURL != ""`, every `LogPushEntry` in the response is POSTed to that URL via `DispatchFeedback`. Trust Wallet's notification-manager-service uses this URL for delivery tracking.

## `PushToAndroid` (FCM)

```go
func PushToAndroid(req *PushNotification, cfg *config.ConfYaml) (*ResponsePush, error)
```

1. Validates message via `CheckMessage`.
2. Initializes an FCM client (per-request API key overrides config key).
3. Builds the `fcm.Message` via `GetAndroidNotification`.
4. Sends; on `fcm.ErrInvalidRegistration` or `fcm.ErrNotRegistered`, marks tokens as failed.
5. Retries up to `cfg.Android.MaxRetry` (or `req.Retry`) on error.

## `PushToIOS` (APNs)

```go
func PushToIOS(req *PushNotification, cfg *config.ConfYaml) (*ResponsePush, error)
```

1. Validates message via `CheckMessage`.
2. Gets or creates an APNs client (pool by cert/key path).
3. Dispatches goroutines per token, throttled by `MaxConcurrentIOSPushes` semaphore channel.
4. On HTTP/2 connection health issues, reconnects using `configureHTTP2ConnHealthCheck`.
5. Retries up to `cfg.Ios.MaxRetry`.

## `PushToHuawei` (HMS)

```go
func PushToHuawei(req *PushNotification, cfg *config.ConfYaml) (*ResponsePush, error)
```

Same retry/log pattern as FCM, but uses Huawei HMS client. AppID/AppSecret can be overridden per-request.

## `configureHTTP2ConnHealthCheck` — Why It's Called 3x

This function configures `ReadIdleTimeout = 1s` and `PingTimeout = 1s` on the APNs HTTP/2 transport. It's called in three places: initial client creation, certificate-based auth setup, and token-based (P8) auth setup. This ensures stale HTTP/2 connections are detected quickly and reconnected rather than silently timing out. The tight timeouts are intentional — APNs drops idle connections and a 1s detection delay is acceptable.

## `CheckMessage` — Validation

`CheckMessage` validates the `PushNotification` struct before dispatch: checks that `Tokens` is non-empty, `Platform` is 1–3, and platform-specific required fields are present. Called by all three push functions.

## See Also
- [architecture/overview.md](overview.md)
- [architecture/data/models.md](data/models.md)
- [features/notify.md](../features/notify.md)
- [credentials](../security/credentials.md) <!-- rel:strong -->
- [push logging](../observability/push-logging.md) <!-- rel:strong -->
