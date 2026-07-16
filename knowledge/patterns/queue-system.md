---
title: Queue System — Async Notification Delivery
category: patterns
tags: [queue, async, golang-queue, nsq, nats, redis]
confidence: high
source: main.go, notify/notification.go, config/config.go
updated: 2026-07-16
---

# Queue System

Gorush uses `golang-queue/queue` for async notification delivery. The queue decouples HTTP ingestion from platform dispatch.

## Queue Worker

Defined via the `Run` closure in `notify/notification.go`:

```go
var Run = func(cfg *config.ConfYaml) func(ctx context.Context, msg queue.QueuedMessage) error {
    return func(ctx context.Context, msg queue.QueuedMessage) error {
        _, err := SendNotification(msg, cfg)
        return err
    }
}
```

The `main.go` passes this to the queue constructor as the worker function.

## Queue Backends

Configured via `cfg.Core.Queue.Engine`:

| Engine | Backend | Notes |
|--------|---------|-------|
| `local` (default) | In-process channel | Simple; no persistence |
| `redis` | go-redis | Persistent; requires Redis |
| `nsq` | golang-queue/nsq | Distributed; requires NSQ daemon |
| `nats` | golang-queue/nats | Distributed; requires NATS server |

## Sync Mode

When `cfg.Core.Sync = true`, the HTTP `pushHandler` waits for all notifications in the request to complete before responding. The cancellable context flows from the HTTP request down through `handleNotification`, so if the client disconnects the pending notifications are cancelled. Default is async (fire-and-forget from the HTTP client's perspective).

## Queue Depth Monitoring

`q.Usage()` returns the current queue depth, exposed as the `gorush_queue_usage` Prometheus gauge via `metric.Metrics.QueueUsage`.

## See Also
- [architecture/overview.md](../architecture/overview.md)
- [architecture/notification-dispatch.md](../architecture/notification-dispatch.md)
- [router engine](../architecture/router-engine.md) <!-- rel:strong -->
- [storage backends](../architecture/storage-backends.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:strong -->
