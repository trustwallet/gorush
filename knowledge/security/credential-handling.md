---
title: "Security: Credential Handling and Token Safety"
category: security
tags: [security, apns, fcm, hms, tokens, credentials, tls]
confidence: high
source: notify/notification_apns.go, notify/notification_fcm.go, config/config.go, logx/log.go
updated: 2026-07-22
---

# Security: Credential Handling and Token Safety

## Platform credentials

| Platform | Credential | How loaded |
|----------|------------|-----------|
| iOS/APNs | `.p8` private key OR `.p12`/`.pem` certificate | File path (`ios.key_path`) or base64 string (`ios.key_base64`) — never written to disk from base64 |
| Android/FCM | API Key | `android.apikey` config value |
| Huawei/HMS | App Secret + App ID | `huawei.appsecret` + `huawei.appid` config values |

Credentials are loaded once at startup by `notify.InitAPNSClient`, `notify.InitFCMClient`, `notify.InitHMSClient`. They are held in package-level variables (`APNSClients`, `FCMClient`, etc.) for the lifetime of the process.

## Device token masking

`cfg.Log.HideToken = true` (default) causes `GetLogPushEntry` to mask device tokens in all log output — the token middle portion is replaced with `***`. This prevents accidental token leakage into log aggregation systems (e.g. Grafana Loki).

**Important:** logs written to external log stores should always have `hide_token: true`. Exposing device tokens would allow unauthorized push targeting.

## TLS configuration

The HTTP server supports:
- Manual TLS via `core.ssl: true` with `core.cert_path` + `core.key_path` (or base64 variants)
- Auto TLS via Let's Encrypt (`core.auto_tls.enabled: true`), storing certs in `core.auto_tls.folder`

APNs always uses HTTP/2 with TLS — `configureHTTP2ConnHealthCheck` sets up the TLS transport with explicit timeout values (`tlsDialTimeout=20s`, `idleConnTimeout=90s`, `tcpKeepAlive=60s`).

## HTTP proxy

`cfg.Core.HTTPProxy` is applied globally to `http.DefaultTransport` via `notify.SetProxy`. This affects FCM calls only (APNs has its own transport). The proxy URL is validated with `url.ParseRequestURI` before being applied.

## Input validation

`CheckMessage` validates all incoming push requests before enqueueing:
- Token count limits enforced per platform (FCM: 1000, HMS: 500)
- Empty token detection
- TimeToLive range validation (FCM: max 4 weeks = 2419200s)

`CheckPushConf` validates config at startup — missing required credentials are a hard error.

## No authentication on the push API

The HTTP push endpoint (`POST /api/push`) has **no built-in authentication** in gorush itself. It relies on network-level access control (private VPC, k8s network policies, or a reverse proxy with auth). Trust Wallet deploys gorush at `gorush.twinternal.net` — accessible only from internal services.

## See Also
- [overview.md](../architecture/overview.md)
- [logging.md](../observability/logging.md)
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
- [configuration](../libs/configuration.md) <!-- rel:strong -->
- [testing strategy](../tests/testing-strategy.md) <!-- rel:related -->
