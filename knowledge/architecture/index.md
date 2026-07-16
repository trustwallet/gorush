# Architecture

> System architecture, module maps, and technical design

## Sections

- [infrastructure/](infrastructure/index.md) — Infrastructure (architecture)

## Documents

| Document | Description | Source |
|----------|-------------|--------|
| [call graph part 2](call-graph-part-2.md) |  | architecture/call-graph.md |
| [call graph](call-graph.md) |  | architecture/call-graph.md |
| [dependency graph](dependency-graph.md) |  |  |
| [grpc server](grpc-server.md) | Gorush exposes a gRPC interface in the `rpc/` package as an alternative to the HTTP API. | rpc/server.go, rpc/proto/ |
| [layers](layers.md) | _No upward-flowing calls detected._ |  |
| [notification dispatch](notification-dispatch.md) | The `notify/` package is the core of gorush. | notify/notification.go, notify/notification_apns.go, notify/notification_fcm.go, notify/notification_hms.go |
| [overview](overview.md) | Gorush is a Go-based push notification server that serves as Trust Wallet's internal push gateway at… | main.go, router/server.go, notify/, config/, storage/ |
| [project structure](project-structure.md) |  |  |
| [request body](request-body.md) | The Request body must have a notifications array. | README.md |
| [router engine](router-engine.md) | `routerEngine` (in `router/server.go:L`) is the most-connected symbol in the codebase (fan-in 3, fan-out 6, degree 9). | router/server.go |
| [storage backends](storage-backends.md) | Gorush tracks push delivery counters (total, iOS/Android/Huawei success and error counts) via a pluggable `Storage`… | storage/storage.go, storage/redis/, storage/memory/, storage/boltdb/, config/config.go |
| [trust wallet deployment](trust-wallet-deployment.md) | Trust Wallet forks and deploys gorush as an internal push notification gateway at `https://gorush.twinternal.net`. | knowledge from org KB, Dockerfile, .github/workflows/, k8s/, helm/ |
