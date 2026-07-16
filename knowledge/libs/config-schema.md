---
title: Configuration Schema (ConfYaml)
category: libs
tags: [config, yaml, confyaml, ios, android, huawei, grpc]
confidence: high
source: config/config.go
updated: 2026-07-16
---

# Configuration Schema (`ConfYaml`)

`ConfYaml` (in `config/config.go:115`) is the root config struct loaded from YAML and env vars via `LoadConf`. Every subsystem takes a `*ConfYaml` pointer at init time.

## Top-Level Sections

| Field | Type | Purpose |
|-------|------|---------|
| `Core` | `SectionCore` | Server behavior: port, mode, PID, queue, feedback URL |
| `API` | `SectionAPI` | URI paths for all HTTP endpoints |
| `Android` | `SectionAndroid` | FCM API key, retry count |
| `Huawei` | `SectionHuawei` | HMS AppID, AppSecret, retry count |
| `Ios` | `SectionIos` | APNs cert/key path, password, KeyID, TeamID, topic, retry |
| `Queue` | `SectionQueue` | Queue engine (redis, nsq, nats, or none) |
| `Log` | `SectionLog` | Access/error log format and file paths |
| `Stat` | `SectionStat` | Storage backend config (Redis, BoltDB, BadgerDB, etc.) |
| `GRPC` | `SectionGRPC` | gRPC server address, enabled flag |

## Key `SectionCore` Fields

| Field | Default | Notes |
|-------|---------|-------|
| `Port` | `8088` | HTTP listen port |
| `MaxNotification` | `100` | Max notifications per request |
| `Sync` | `false` | If true, HTTP handler waits for delivery completion |
| `Mode` | `release` | Gin mode (release/debug) |
| `FeedbackURL` | `""` | Upstream delivery callback; Trust Wallet sets this |
| `AutoTLS.Enabled` | `false` | Let's Encrypt auto-TLS |
| `Queue.Engine` | `local` | Queue type: local/redis/nsq/nats |

## `SectionIos` — APNs Auth

Two auth modes:
- **Certificate** (`KeyPath` + `Password`): p12 cert file
- **Token** (`KeyPath` + `KeyID` + `TeamID`): p8 token file (preferred for Trust Wallet)

The topic (`SectionIos.Topic`) maps to the app bundle ID.

## Environment Variable Override

`LoadConf` uses Viper's env binding, so any nested config key can be overridden via env:
```
GORUSH_CORE_PORT=8088
GORUSH_ANDROID_APIKEY=<key>
GORUSH_IOS_KEYPATH=/certs/key.p8
```

## See Also
- [architecture/overview.md](../architecture/overview.md)
- [security/secrets/send-huawei-hms-notification.md](../security/secrets/send-huawei-hms-notification.md)
- [models](../architecture/data/models.md) <!-- rel:strong -->
- [credentials](../security/credentials.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:related -->
