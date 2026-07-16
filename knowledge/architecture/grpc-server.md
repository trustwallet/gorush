---
title: gRPC Server — Push via RPC
category: architecture
tags: [grpc, rpc, proto, send, health-check]
confidence: high
source: rpc/server.go, rpc/proto/
updated: 2026-07-16
---

# gRPC Server

Gorush exposes a gRPC interface in the `rpc/` package as an alternative to the HTTP API. It runs on its own address/port (`cfg.GRPC.Addr`) and can run simultaneously with the HTTP server.

## Services

### `Health` (standard gRPC health protocol)

```proto
Check(HealthCheckRequest) → HealthCheckResponse
```

Returns `SERVING` for the overall server, or looks up per-service status in the `statusMap`. Returns `NotFound` for unknown services. Used for k8s readiness probes.

### `Gorush` (push delivery)

```proto
Send(NotificationRequest) → NotificationReply
```

Accepts the same logical fields as the HTTP API (`tokens`, `platform`, `message`, `badge`, `title`, `topic`, `category`, `sound`) and builds a `notify.PushNotification`, then calls `SendNotification` directly (not via queue). Returns `ok: true` with the count of tokens sent.

## Trust Wallet Usage

Trust Wallet's notification-manager-service can use the gRPC path for low-latency delivery bypassing the HTTP queue. The Node.js client in `rpc/example/node/` demonstrates usage. This is the `rpc` domain in `.relations.json`.

## See Also
- [architecture/overview.md](overview.md)
- [features/rpc.md](../features/rpc.md)
- [config schema](../libs/config-schema.md) <!-- rel:strong -->
- [credentials](../security/credentials.md) <!-- rel:strong -->
- [queue system](../patterns/queue-system.md) <!-- rel:strong -->
