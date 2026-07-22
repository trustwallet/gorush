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
| [grpc interface](grpc-interface.md) | Gorush exposes an optional gRPC server alongside its HTTP API. | rpc/, doc.go |
| [layers](layers.md) | _No upward-flowing calls detected._ |  |
| [notification dispatch](notification-dispatch.md) | `routerEngine` in `router/server.go` is the single function that assembles the entire Gin HTTP router: it configures… | notify/notification.go, notify/notification_apns.go, notify/notification_fcm.go, notify/notification_hms.go, router/server.go |
| [overview](overview.md) | Gorush is a push notification gateway server that accepts a unified JSON request body and fans out to platform-specific… | main.go, router/server.go, notify/notification.go, config/config.go |
| [project structure](project-structure.md) |  |  |
| [queue processing](queue-processing.md) | Gorush uses `github.com/golang-queue/queue` as its queue abstraction. | main.go, notify/notification.go |
| [request body](request-body.md) | The Request body must have a notifications array. | README.md |
