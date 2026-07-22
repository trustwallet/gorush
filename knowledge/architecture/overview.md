---
title: "Gorush Architecture Overview"
category: architecture
tags: [gorush, push-notification, ios, android, huawei, gin, queue]
confidence: high
source: main.go, router/server.go, notify/notification.go, config/config.go
updated: 2026-07-22
---

# Gorush Architecture Overview

Gorush is a push notification gateway server that accepts a unified JSON request body and fans out to platform-specific push services: Apple APNs (iOS), Google FCM (Android), and Huawei HMS.

## High-level shape

```
HTTP client / gRPC client
        │
        ▼
   router/server.go          ← Gin HTTP server (routerEngine builds all routes)
        │
        ▼
  Queue (local|NSQ|NATS)     ← Async notification queue; sync mode bypasses wait
        │
        ▼
  notify/notification.go     ← SendNotification dispatches by platform field
        │
     ┌──┼──────────────┐
     ▼  ▼              ▼
  APNs FCM           HMS
  (iOS)(Android) (Huawei)
        │
        ▼
  logx / status / metric     ← Structured logging, stats storage, Prometheus
```

## Layers

| Layer | Package | Responsibility |
|-------|---------|----------------|
| Entry point | `main.go` | CLI flags, queue wiring, graceful shutdown with `errgroup` |
| HTTP API | `router/` | Gin engine, all REST endpoints, request validation |
| Push dispatch | `notify/` | Platform routing, APNS/FCM/HMS clients, feedback hooks |
| Configuration | `config/` | YAML config via viper; `ConfYaml` is the central config struct |
| Logging | `logx/` | Zerolog-based access + error logs; `LogPushEntry` per notification |
| Metrics | `metric/` | Prometheus custom metrics (queue depth, push counts) |
| Statistics | `status/` | App-level counters (success/error per platform) |
| Storage | `storage/` | Counter backends: memory, Redis, BoltDB, BuntDB, LevelDB |
| gRPC | `rpc/` | Optional gRPC server on configurable port (default 9000) |

## Entry point: `main.go`

`main` parses CLI flags into a partial `ConfYaml`, loads the YAML config file, wires the queue backend (local / NSQ / NATS), initializes APNs/FCM/Huawei clients, starts the HTTP server and optional gRPC server, then blocks on `errgroup` with OS signal handling for graceful shutdown.

## HTTP API surface

All routes are registered in `routerEngine` (`router/server.go`):

| Method | Path | Handler |
|--------|------|---------|
| POST | `/api/push` | `pushHandler` — accepts batched push requests |
| GET | `/api/stat/app` | App push stats |
| GET | `/api/stat/go` | Go runtime stats |
| GET | `/api/config` | Running config YAML |
| GET | `/sys/stats` | HTTP stats middleware data |
| GET | `/metrics` | Prometheus metrics |
| GET | `/healthz` | Heartbeat (200 OK) |
| HEAD | `/healthz` | Heartbeat |
| GET | `/version` | Version string |
| GET | `/` | Welcome message |

## Push dispatch

`SendNotification` in `notify/notification.go` is the dispatch hub. It unwraps a `QueuedMessage` to a `PushNotification` struct and switches on `Platform`:

- `1` (iOS) → `PushToIOS`
- `2` (Android) → `PushToAndroid`
- `3` (Huawei) → `PushToHuawei`

After dispatch it calls `DispatchFeedback` if `cfg.Core.FeedbackURL` is set, posting push results to a webhook.

## Queue backends

| Backend | Config value | Notes |
|---------|-------------|-------|
| In-process | `local` | Default; no external dependency |
| NSQ | `nsq` | Distributed messaging; configured at `queue.nsq.*` |
| NATS | `nats` | Lightweight pub/sub; configured at `queue.nats.*` |

## Sync vs async mode

`cfg.Core.Sync = false` (default): push requests are enqueued and the HTTP response returns immediately with a count. `Sync = true`: the handler waits for notification processing before responding, and client disconnect cancels the context so in-flight notifications are aborted.

## See Also
- [notification-dispatch.md](notification-dispatch.md)
- [queue-processing.md](queue-processing.md)
- [call-graph.md](call-graph.md)
- [layers.md](layers.md)
- [storage backends](../observability/storage-backends.md) <!-- rel:strong -->
