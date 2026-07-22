---
title: "gRPC Interface"
category: architecture
tags: [grpc, rpc, protobuf, api]
confidence: high
source: rpc/, doc.go
updated: 2026-07-22
---

# gRPC Interface

Gorush exposes an optional gRPC server alongside its HTTP API. It is disabled by default (`grpc.enabled: false`) and listens on port 9000 when enabled.

## Configuration

```yaml
grpc:
  enabled: false
  port: 9000
```

## Proto definition

The `rpc/` directory contains the protobuf definition and generated Go code. The service mirrors the HTTP push API — clients can submit `PushNotification` messages via gRPC instead of HTTP.

## Client examples

The `rpc/example/node/` directory contains Node.js gRPC client example code (`client.js`, `gorush_grpc_pb.js`, `gorush_pb.js`), demonstrating how to call gorush's push service via gRPC from JavaScript.

## When to use gRPC vs HTTP

The gRPC interface is useful for:
- Lower-latency internal service-to-service calls (no JSON parsing overhead)
- Strongly-typed contracts via protobuf
- Streaming push batches

The HTTP REST API (`POST /api/push`) is the primary interface used by Trust Wallet's internal services (see org KB: `gorush-push-notification-api`).

## See Also
- [overview.md](overview.md)
- [backend/api-endpoints.md](backend/api-endpoints.md)
- [credential handling](../security/credential-handling.md) <!-- rel:strong -->
- [configuration](../libs/configuration.md) <!-- rel:strong -->
- [testing strategy](../tests/testing-strategy.md) <!-- rel:strong -->
