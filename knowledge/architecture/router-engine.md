---
title: routerEngine — Central HTTP Router
category: architecture
tags: [router, gin, http, middleware, prometheus]
confidence: high
source: router/server.go
updated: 2026-07-16
---

# `routerEngine` — Central HTTP Router

`routerEngine` (in `router/server.go:L`) is the most-connected symbol in the codebase (fan-in 3, fan-out 6, degree 9). It constructs and returns the configured `*gin.Engine` that handles all HTTP traffic.

## Contract

```go
func routerEngine(cfg *config.ConfYaml, q *queue.Queue) *gin.Engine
```

**Input**: The global config and the active notification queue.  
**Output**: A fully-wired Gin engine ready to `ListenAndServe`.

## What It Wires

| Route | Handler | Notes |
|-------|---------|-------|
| `POST cfg.API.PushURI` | `pushHandler(cfg, q)` | Core delivery endpoint |
| `GET cfg.API.StatGoURI` | `api.GinHandler` | Go runtime stats |
| `GET cfg.API.StatAppURI` | `appStatusHandler(q)` | App-level push counters |
| `GET cfg.API.ConfigURI` | `configHandler(cfg)` | Dumps running config |
| `GET cfg.API.SysStatURI` | `sysStatsHandler()` | System stats |
| `GET cfg.API.MetricURI` | `metricsHandler` | Prometheus metrics |
| `GET/HEAD cfg.API.HealthURI` | `heartbeatHandler` | Health check (k8s probe) |
| `GET /version` | `versionHandler` | Version string |
| `GET /` | `rootHandler` | Welcome message |

## Middleware Stack (in order)

1. **`logger.SetLogger`** — zerolog request logger (skips health and metrics URIs to avoid noise)
2. **`gin.Recovery`** — panic recovery → 500 response
3. **`VersionMiddleware`** — injects server version header
4. **`StatMiddleware`** — updates the `stats` counters (request counts, status codes)

## Prometheus Registration (once)

Uses `sync.Once` to register the `metric.Metrics` descriptor exactly once, even if `routerEngine` is called multiple times in tests. The `QueueUsage` gauge reads live queue depth via a closure over `q`.

## Why It's Central

Three callers depend on it: `RunHTTPServer` (normal mode), `RunHTTPSServer` (TLS mode), and `RunAutoTLSServer` (Let's Encrypt). All HTTP traffic, auth, and metrics flow through the router engine it returns.

## See Also
- [features/router.md](../features/router.md)
- [architecture/overview.md](overview.md)
- [queue system](../patterns/queue-system.md) <!-- rel:strong -->
- [push logging](../observability/push-logging.md) <!-- rel:related -->
- [features](../observability/alerting/features.md) <!-- rel:related -->
