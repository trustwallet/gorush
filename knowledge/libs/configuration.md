---
title: "Configuration Reference (ConfYaml)"
category: libs
tags: [config, yaml, viper, confyaml]
confidence: high
source: config/config.go
updated: 2026-07-22
---

# Configuration Reference (ConfYaml)

Gorush is configured via a YAML file (flag `-c` or `--config`). The struct is `config.ConfYaml`.

## Core section

| Key | Default | Notes |
|-----|---------|-------|
| `core.enabled` | true | Enable HTTP server |
| `core.address` | "" | Bind address (empty = all interfaces) |
| `core.port` | "8088" | HTTP port (ignored if `auto_tls.enabled`) |
| `core.worker_num` | `runtime.NumCPU()` | Queue worker goroutines |
| `core.queue_num` | 8192 | Queue buffer size |
| `core.max_notification` | 100 | Max notifications per single POST request |
| `core.sync` | false | Wait for push before HTTP response |
| `core.feedback_hook_url` | "" | Webhook for async push result delivery |
| `core.feedback_timeout` | 10 | Feedback webhook timeout (seconds) |
| `core.mode` | "release" | "debug" or "release" |
| `core.shutdown_timeout` | 30 | Graceful shutdown timeout (seconds) |
| `core.ssl` | false | Enable TLS (uses cert/key paths) |
| `core.http_proxy` | "" | HTTP proxy for FCM calls |
| `core.auto_tls.enabled` | false | Let's Encrypt auto TLS |

## Platform sections

### `ios`
| Key | Notes |
|-----|-------|
| `key_path` | Path to `.p8`, `.p12`, or `.pem` certificate |
| `key_base64` | Base64-encoded key (alternative to path) |
| `key_type` | "pem", "p12", or "p8" |
| `password` | Certificate password |
| `production` | false = sandbox, true = production APNs |
| `max_concurrent_pushes` | 100 |
| `max_retry` | Retry count for failed pushes |
| `key_id` | P8 Key ID (from Apple Developer account) |
| `team_id` | P8 Team ID (from Apple Developer account) |

### `android`
| Key | Notes |
|-----|-------|
| `apikey` | Firebase Server Key |
| `max_retry` | Retry count for failed pushes |

### `huawei`
| Key | Notes |
|-----|-------|
| `appsecret` | HMS App Secret |
| `appid` | HMS App ID |
| `max_retry` | Retry count |

## Queue section

```yaml
queue:
  engine: "local"   # local | nsq | nats
  nsq:
    addr: 127.0.0.1:4150
    topic: gorush
    channel: gorush
  nats:
    addr: 127.0.0.1:4222
    subj: gorush
    queue: gorush
```

## API URI customization

All API paths are configurable:

```yaml
api:
  push_uri: "/api/push"
  stat_go_uri: "/api/stat/go"
  stat_app_uri: "/api/stat/app"
  config_uri: "/api/config"
  sys_stat_uri: "/sys/stats"
  metric_uri: "/metrics"
  health_uri: "/healthz"
```

## Stat engine

```yaml
stat:
  engine: "memory"   # memory | redis | boltdb | buntdb | leveldb
  redis:
    addr: "localhost:6379"
```

## Log section

```yaml
log:
  format: "string"          # string | json
  access_log: "stdout"
  access_level: "debug"
  error_log: "stderr"
  error_level: "error"
  hide_token: true           # mask device tokens in logs
```

## See Also
- [overview.md](../architecture/overview.md)
- [storage-backends.md](../observability/storage-backends.md)
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
- [credential handling](../security/credential-handling.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:strong -->
