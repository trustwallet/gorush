---
title: Logging — LogPushEntry and GetLogPushEntry
category: observability
tags: [logging, logpush, zerolog, structured-logs]
confidence: high
source: logx/log.go
updated: 2026-07-16
---

# Push Logging (`logx`)

The `logx` package provides structured push-result logging via zerolog. It is the central observation point for delivery outcomes.

## `GetLogPushEntry` — Central Log Builder

```go
func GetLogPushEntry(input *InputLog) LogPushEntry
```

This function (fan-out 2 — called by all three platform push functions) builds a `LogPushEntry` from an `InputLog`. It:
- Maps the numeric platform to a string (`ios`, `android`, `huawei`) via `typeForPlatForm`
- Trims the token to 10 chars if `HideToken == true` (protecting PII in logs)
- Converts the error to a string for JSON serialization

## `LogPushEntry` Structure

```go
type LogPushEntry struct {
    ID       string  // notification ID
    Type     string  // "success" or "fail"
    Platform string  // "ios", "android", "huawei"
    Token    string  // device token (possibly masked)
    Message  string  // notification body
    Error    string  // error string if failed
}
```

These entries are returned in `ResponsePush.Logs` from the HTTP API and POSTed to `FeedbackURL` for upstream tracking.

## `LogAccess` vs `LogError`

Two zerolog logger instances:
- `LogAccess` — request-level logs (debug/info for normal flow)
- `LogError` — error-level logs for delivery failures

## `colorForPlatForm` vs `typeForPlatForm`

- `typeForPlatForm` returns the string name used in `LogPushEntry.Platform` and in Prometheus labels.
- `colorForPlatForm` returns a terminal color code for human-readable console output.

## See Also
- [architecture/notification-dispatch.md](../architecture/notification-dispatch.md)
- [observability/alerting/features.md](alerting/features.md)
- [credentials](../security/credentials.md) <!-- rel:strong -->
- [overview](../architecture/overview.md) <!-- rel:strong -->
- [router engine](../architecture/router-engine.md) <!-- rel:strong -->
