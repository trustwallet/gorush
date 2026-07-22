---
title: "Testing Strategy"
category: tests
tags: [testing, unit-tests, integration, fcm, apns, hms]
confidence: high
source: notify/*_test.go, tests/
updated: 2026-07-22
---

# Testing Strategy

## Test coverage

The `notify/` package has comprehensive unit tests:
- `notification_test.go` — `CheckMessage` validation tests
- `notification_apns_test.go` — APNs push logic tests (with mock APNs server)
- `notification_fcm_test.go` — FCM push logic tests
- `notification_hms_test.go` — HMS push logic tests
- `feedback_test.go` — Feedback webhook tests
- `main_test.go` — Package-level setup

## Test helpers

`notify/global.go` exposes test-facing initialization (shared APNs client state). Tests typically:
1. Build a `ConfYaml` with `Enabled: true` and test credentials
2. Call `InitAPNSClient`/`InitFCMClient`/`InitHMSClient`
3. Construct `PushNotification` structs
4. Assert on response/error

## Integration tests

`tests/` directory contains integration-level test resources. Full end-to-end testing requires valid APNs/FCM/HMS credentials — these tests are skipped by default without real credentials.

## Memory usage tests

`knowledge/tests/memory-usage.md` (migrated from README) documents memory profiling patterns for the running server.

## Running tests

```bash
go test ./...                          # all unit tests
go test -v ./notify/...                # notify package verbose
go test -run TestPushToAndroid ./notify/
```

## See Also
- [overview.md](../architecture/overview.md)
- [build/build-gorush-binary.md](../build/build-gorush-binary.md)
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
- [credential handling](../security/credential-handling.md) <!-- rel:strong -->
- [notify](../features/notify.md) <!-- rel:strong -->
