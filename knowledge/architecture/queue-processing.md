---
title: "Queue Processing and Worker Lifecycle"
category: architecture
tags: [queue, nsq, nats, workers, async, lifecycle]
confidence: high
source: main.go, notify/notification.go
updated: 2026-07-22
---

# Queue Processing and Worker Lifecycle

## Queue topology

Gorush uses `github.com/golang-queue/queue` as its queue abstraction. The main function wires a concrete backend:

```
main.go
  ├── engine="local" → queue.NewRing (in-process ring buffer)
  ├── engine="nsq"   → nsq.NewWorker (NSQ distributed messaging)
  └── engine="nats"  → nats.NewWorker (NATS pub/sub)
```

Workers are created with `queue.WithWorkerCount(cfg.Core.WorkerNum)` (defaults to `runtime.NumCPU()`) and queue capacity `queue.WithQueueSize(cfg.Core.QueueNum)` (defaults to 8192).

## Worker function

The queue worker function is `notify.Run(cfg)`, which returns a closure:

```go
func(ctx context.Context, msg queue.QueuedMessage) error {
    _, err := SendNotification(msg, cfg)
    return err
}
```

Each dequeued message is deserialized to `PushNotification` and dispatched to the appropriate platform handler.

## Sync vs async modes

| Mode | Behaviour |
|------|-----------|
| `sync: false` (default) | `pushHandler` enqueues notifications and returns `200 OK` immediately with counts. Client never waits for actual delivery. |
| `sync: true` | A goroutine watches `c.Request.Context().Done()`. If the client disconnects, the context is cancelled, which stops in-progress `PushToIOS/Android/Huawei` calls. The handler returns only after all notifications finish. |

**When to use sync mode:** useful for small-scale testing or webhook-driven flows that need delivery confirmation in the HTTP response. Not recommended for high-throughput because it ties HTTP connections to push latency.

## Graceful shutdown

`main.go` uses `golang.org/x/sync/errgroup` with a custom context that listens for `SIGINT`/`SIGTERM`. On shutdown:

1. Context is cancelled.
2. HTTP server calls `Shutdown(ctx)` with a `cfg.Core.ShutdownTimeout` deadline (default 30s).
3. Queue is stopped, flushing in-flight messages before exit.

## Queue message format

`PushNotification` implements `queue.QueuedMessage` via its `Bytes()` method, which JSON-marshals the struct. Workers deserialize with `json.Unmarshal`. This means the queue can be backed by an external broker (NSQ/NATS) and messages survive a restart if the broker persists them.

## See Also
- [overview.md](overview.md)
- [notification-dispatch.md](notification-dispatch.md)
- [configuration](../libs/configuration.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:strong -->
- [storage backends](../observability/storage-backends.md) <!-- rel:strong -->
