---
title: "Statistics Storage Backends"
category: observability
tags: [storage, redis, boltdb, buntdb, leveldb, counters, stats]
confidence: high
source: storage/, status/
updated: 2026-07-22
---

# Statistics Storage Backends

Gorush tracks push success/error counts per platform. The `status` package owns `StatStorage`, an interface with backend-swappable implementations.

## Backends

| Engine config | Implementation | Notes |
|--------------|----------------|-------|
| `memory` (default) | In-process atomic counters | Fast, lost on restart |
| `redis` | Redis SET via `go-redis` | Persists across restarts; configure `stat.redis.*` |
| `boltdb` | BoltDB embedded KV | Single-file DB; persistent, no external dependency |
| `buntdb` | BuntDB in-memory KV | Optional persistence to file |
| `leveldb` | LevelDB embedded KV | Persistent, no external dependency |

## Counters tracked

- `TotalCount` — total push attempts
- `IosSuccess` / `IosError`
- `AndroidSuccess` / `AndroidError`
- `HuaweiSuccess` / `HuaweiError`

Counters are incremented after each individual token push result, inside `PushToIOS`, `PushToAndroid`, `PushToHuawei`.

## App stats API

`GET /api/stat/app` exposes counters via `appStatusHandler` (in `router/server.go`), which reads from `status.StatStorage`. Also exposes queue capacity/usage.

## See Also
- [overview.md](../architecture/overview.md)
- [get-metrics.md](metrics/get-metrics.md)
- [models](../architecture/data/models.md) <!-- rel:strong -->
- [call graph](../architecture/call-graph.md) <!-- rel:strong -->
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
