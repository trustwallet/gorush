---
title: Storage Backends — Pluggable Counter Store
category: architecture
tags: [storage, redis, boltdb, badgerdb, metrics, counters]
confidence: high
source: storage/storage.go, storage/redis/, storage/memory/, storage/boltdb/, config/config.go
updated: 2026-07-16
---

# Storage Backends

Gorush tracks push delivery counters (total, iOS/Android/Huawei success and error counts) via a pluggable `Storage` interface. The active backend is wired through the global `status` package.

## `Storage` Interface

Defined in `storage/storage.go`:

```go
type Storage interface {
    Init() error
    Reset()
    AddTotalCount(int64)
    AddIosSuccess(int64)
    AddIosError(int64)
    AddAndroidSuccess(int64)
    AddAndroidError(int64)
    AddHuaweiSuccess(int64)
    AddHuaweiError(int64)
    GetTotalCount() int64
    GetIosSuccess() int64
    // ... etc
    Close() error
}
```

## Available Backends

| Backend | Package | Config key | Notes |
|---------|---------|-----------|-------|
| In-memory | `storage/memory` | `core.stat_go_uri` stat type | Default; lost on restart |
| Redis | `storage/redis` | `core.store = "redis"` | Requires `stat.redis.*` config; persistent |
| BoltDB | `storage/boltdb` | `core.store = "boltdb"` | Embedded file-based KV |
| BuntDB | `storage/buntdb` | `core.store = "buntdb"` | Embedded in-memory/file KV |
| LevelDB | `storage/leveldb` | `core.store = "leveldb"` | Embedded; file-based |
| BadgerDB | `storage/badger` | `core.store = "badgerdb"` | Embedded; file-based, high perf |

## Counter Keys

Each backend stores counters under fixed string keys from `storage/storage.go`:

```
gorush-total-count
gorush-ios-success-count / gorush-ios-error-count
gorush-android-success-count / gorush-android-error-count
gorush-huawei-success-count / gorush-huawei-error-count
```

## Prometheus Integration

The `metric.Metrics` struct reads from `status` (which reads from the active storage backend) to expose `gorush_*` Prometheus gauges. The Grafana dashboard at `https://monitoring.twinternal.net/d/z1WA0STGk/gorush` visualizes these.

## Trust Wallet Usage

Trust Wallet's deployment uses Redis storage for persistence across pod restarts on Heroku/k8s, backed by the `stat.redis.*` config section.

## See Also
- [features/storage.md](../features/storage.md)
- [observability/metrics/get-metrics.md](../observability/metrics/get-metrics.md)
- [queue system](../patterns/queue-system.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:strong -->
- [config schema](../libs/config-schema.md) <!-- rel:strong -->
