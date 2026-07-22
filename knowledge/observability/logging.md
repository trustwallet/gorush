---
title: "Logging: logx and GetLogPushEntry"
category: observability
tags: [logging, zerolog, push-log, structured-log]
confidence: high
source: logx/log.go, notify/notification_fcm.go, notify/notification_apns.go
updated: 2026-07-22
---

# Logging: logx and GetLogPushEntry

## Log structure

The `logx` package exposes two loggers:
- `LogAccess` — HTTP access log (stdout by default, format: string or JSON)
- `LogError` — Error log (stderr by default)

Both are zerolog `Logger` instances. `InitLog(cfg)` configures output destinations and levels from config.

## LogPushEntry

`LogPushEntry` is the structured log record for each push attempt:

```go
type LogPushEntry struct {
    ID       string    // notification ID (notif_id field)
    Token    string    // device token (may be masked if HideToken=true)
    Platform string    // "ios", "android", "huawei"
    Message  string    // notification message body
    Error    string    // error string, empty on success
    Success  bool
    Time     time.Time
}
```

## GetLogPushEntry — fan-in 3

`GetLogPushEntry` (fan-in 3) is the factory that creates a `LogPushEntry` from a `PushNotification` + result. It is called from all three platform handlers after each individual token dispatch:
- `logPush` in `notification_fcm.go` (success, partial-failure, retry)
- The corresponding helpers in `notification_apns.go` and `notification_hms.go`

This makes it the central point for normalizing push log data. Any change to the log schema goes here.

**Token masking:** if `cfg.Log.HideToken` is true (default: true), `GetLogPushEntry` replaces the middle portion of the device token with `***` before logging, preventing token leakage in logs.

## logPush (FCM)

`logPush` in `notification_fcm.go` has fan-in 3 — it is called from the FCM success path, the partial-failure path (some tokens failed), and the retry path. It writes a `LogPushEntry` to `LogAccess` and increments `status.StatStorage` counters.

## See Also
- [get-metrics.md](../observability/metrics/get-metrics.md)
- [overview.md](../architecture/overview.md)
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
- [credential handling](../security/credential-handling.md) <!-- rel:strong -->
- [call graph](../architecture/call-graph.md) <!-- rel:related -->
