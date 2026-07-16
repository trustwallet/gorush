---
title: Gorush Architecture Overview
category: architecture
tags: [gorush, push-notification, architecture, overview]
confidence: high
source: main.go, router/server.go, notify/, config/, storage/
updated: 2026-07-16
---

# Gorush Architecture Overview

Gorush is a Go-based push notification server that serves as Trust Wallet's internal push gateway at `https://gorush.twinternal.net`. It accepts unified JSON payloads and dispatches notifications to iOS (APNs), Android (FCM), and Huawei (HMS) platforms.

## High-Level Flow

```
HTTP POST /api/push
      │
      ▼
pushHandler (router/server.go)
      │  validates request, enforces MaxNotification limit
      ▼
handleNotification (router/server.go)
      │  enqueues each PushNotification to golang-queue/queue
      ▼
SendNotification (notify/notification.go)
      │  dispatches by platform field:
      ├── platform=1 → PushToIOS (APNs)
      ├── platform=2 → PushToAndroid (FCM)
      └── platform=3 → PushToHuawei (HMS)
```

## Layers

| Layer | Packages | Responsibility |
|-------|----------|----------------|
| **Entry** | `main.go` | CLI flags, config load, queue init, signal handling, HTTP + gRPC server start |
| **Routing** | `router/` | Gin HTTP routes, middleware, Prometheus metrics endpoint |
| **Notification** | `notify/` | Platform dispatch, payload building, retry logic |
| **Config** | `config/` | YAML config parsing, all platform credentials |
| **Storage** | `storage/` | Pluggable counter store (in-memory, Redis, BoltDB, LevelDB, BadgerDB, BuntDB) |
| **Status** | `status/` | Global counter state wired to storage backend |
| **Metrics** | `metric/` | Prometheus descriptor registration |
| **Logging** | `logx/` | Structured push log entries, zerolog wrappers |
| **RPC** | `rpc/` | gRPC server exposing the same Send + Health API |

## Key Design Decisions

- **Queue-based async dispatch**: Notifications are enqueued via `golang-queue/queue` rather than handled synchronously. The `cfg.Core.Sync` flag optionally enables synchronous mode where the HTTP handler waits for delivery before responding.
- **Pluggable storage backends**: `storage.Storage` is an interface with 6 backends (memory, Redis, BoltDB, BuntDB, LevelDB, BadgerDB). The backend is chosen by config and the global `status` package holds the active instance.
- **Dual transport**: HTTP (Gin) and gRPC (`rpc/`) servers can run simultaneously, sharing the same queue and config.
- **Feedback URL**: If `cfg.Core.FeedbackURL` is set, every push result is POST-ed back to that URL for upstream delivery tracking (used by Trust Wallet's notification-manager-service).

## See Also
- [features/notify.md](../features/notify.md) — platform dispatch detail
- [features/router.md](../features/router.md) — HTTP server and route config
- [libs/config.md](../libs/config.md) — configuration schema
- [features/storage.md](../features/storage.md) — counter storage backends
- [config schema](../libs/config-schema.md) <!-- rel:strong -->
