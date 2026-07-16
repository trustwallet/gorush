---
category: architecture
confidence: low
documentType: explanation
scope: repo
contentHash: 47bf09dfe770
tags: [architecture, domain, dependency]
source: architecture/call-graph.md
verified: 2026-07-16
splitPartIndex: 2
splitPartTotal: 2
canonical: false
synthetic: split-part
---

## Call Graph (Part 2)

- Call edges: **50** across **259** symbols
- Reachable from entry points (exported symbols + routes): **227**
- Dependency cycles: **0**
- Cross-domain bridges: **0**
- Dead-code candidates (non-exported, zero callers, unreachable): **29**

### Most-coupled symbols (god-node ranking)

| Symbol | Fan-in | Fan-out | Degree |
|--------|--------|---------|--------|
| `routerEngine` | 3 | 6 | 9 |
| `PushToAndroid` | 1 | 4 | 5 |
| `PushToHuawei` | 1 | 4 | 5 |
| `PushToIOS` | 1 | 3 | 4 |
| `SendNotification` | 0 | 4 | 4 |
| `GetLogPushEntry` | 1 | 2 | 3 |
| `main` | 0 | 3 | 3 |
| `configureHTTP2ConnHealthCheck` | 3 | 0 | 3 |
| `InitAPNSClient` | 0 | 3 | 3 |
| `logPush` | 3 | 0 | 3 |
| `RunHTTPServer` | 0 | 3 | 3 |
| `startServer` | 1 | 2 | 3 |
| `pushHandler` | 1 | 2 | 3 |
| `InitLog` | 0 | 2 | 2 |
| `LogPush` | 0 | 2 | 2 |

### Possible duplicate entities (name variants)

> Symbol names that normalize identically — likely the same entity spelled inconsistently. Unify or distinguish in the docs.

- `GET /version` / `GetVersion`
- `Init` / `init`
- `LogPush` / `logPush`

### Dead-code candidates

> Non-exported symbols with no resolved callers, unreachable from any entry point. Static analysis cannot see dynamic dispatch — verify before removing.

- `init` (`logx/log.go`)
- `main` (`main.go`)
- `usage` (`main.go`)
- `heartbeatHandler` (`router/server.go`)
- `metricsHandler` (`router/server.go`)
- `rootHandler` (`router/server.go`)
- `versionHandler` (`router/server.go`)
- `healthClient` (`rpc/client_grpc_health.go`)
- `main` (`rpc/example/go/health/main.go`)
- `main` (`rpc/example/go/send/main.go`)
- `main` (`rpc/example/node/client.js`)
- `deserialize_proto_HealthCheckRequest` (`rpc/example/node/gorush_grpc_pb.js`)
- `deserialize_proto_HealthCheckResponse` (`rpc/example/node/gorush_grpc_pb.js`)
- `deserialize_proto_NotificationReply` (`rpc/example/node/gorush_grpc_pb.js`)
- `deserialize_proto_NotificationRequest` (`rpc/example/node/gorush_grpc_pb.js`)
- `serialize_proto_HealthCheckRequest` (`rpc/example/node/gorush_grpc_pb.js`)
- `serialize_proto_HealthCheckResponse` (`rpc/example/node/gorush_grpc_pb.js`)
- `serialize_proto_NotificationReply` (`rpc/example/node/gorush_grpc_pb.js`)
- `serialize_proto_NotificationRequest` (`rpc/example/node/gorush_grpc_pb.js`)
- `getBadger` (`storage/badger/badger.go`)
- `setBadger` (`storage/badger/badger.go`)
- `getBoltDB` (`storage/boltdb/boltdb.go`)
- `setBoltDB` (`storage/boltdb/boltdb.go`)
- `getBuntDB` (`storage/buntdb/buntdb.go`)
- `setBuntDB` (`storage/buntdb/buntdb.go`)
- `getLevelDB` (`storage/leveldb/leveldb.go`)
- `setLevelDB` (`storage/leveldb/leveldb.go`)
- `statApp` (`storage/memory/memory.go`)
- `getInt64` (`storage/redis/redis.go`)

## See Also
- [notify](../features/notify.md) <!-- rel:strong -->
- [storage](../features/storage.md) <!-- rel:strong -->
- [router](../features/router.md) <!-- rel:strong -->
- [rpc](../features/rpc.md) <!-- rel:strong -->
- [logx](../features/logx.md) <!-- rel:strong -->
