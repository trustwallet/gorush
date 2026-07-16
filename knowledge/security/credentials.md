---
title: Security — API Keys, Certificates, and Secrets Handling
category: security
tags: [security, apns, fcm, hms, api-key, certificate, p8, p12]
confidence: high
source: config/config.go, notify/notification_apns.go, notify/notification_fcm.go
updated: 2026-07-16
---

# Security — API Keys and Credentials

Gorush handles several categories of secrets for push delivery. All secrets are passed via config YAML or environment variables — never hardcoded.

## Credential Types

| Platform | Secret | Config Path | Notes |
|----------|--------|-------------|-------|
| iOS APNs (cert) | p12 certificate + password | `ios.key_path`, `ios.password` | File path only; cert read at startup |
| iOS APNs (token) | p8 private key | `ios.key_path` | Preferred; no expiry unlike certs |
| iOS APNs (token) | KeyID + TeamID | `ios.key_id`, `ios.team_id` | Identifies the developer account |
| Android FCM | Server API key | `android.api_key` | Can be overridden per-notification |
| Huawei HMS | AppID + AppSecret | `huawei.app_id`, `huawei.app_secret` | Can be overridden per-notification |

## Token Masking

`logx.hideToken(token, 10)` masks device tokens in log output to show only the first/last 10 chars, protecting device token PII. This is controlled by `cfg.Log.HideToken` and enforced in `GetLogPushEntry`.

## Per-Request Key Override

Both `android.api_key` and `huawei.app_id`/`app_secret` can be overridden per notification in the push payload. This allows multi-tenant usage of a single gorush instance — different apps can provide their own credentials. However, it requires callers to have their own credentials, which Trust Wallet's deployment does NOT expose; the config-level keys are used exclusively.

## HTTP/2 Health and TLS

APNs uses HTTP/2 over TLS. The `configureHTTP2ConnHealthCheck` function sets `ReadIdleTimeout` and `PingTimeout` to 1s to quickly detect dropped connections — a security hygiene measure preventing token reuse on stale connections.

## AutoTLS

Gorush supports Let's Encrypt (`core.auto_tls.enabled`) for HTTPS if deployed directly to the internet. Trust Wallet uses load balancer TLS termination instead.

## See Also
- [libs/config-schema.md](../libs/config-schema.md)
- [security/secrets/send-huawei-hms-notification.md](secrets/send-huawei-hms-notification.md)
- [notification dispatch](../architecture/notification-dispatch.md) <!-- rel:strong -->
- [push logging](../observability/push-logging.md) <!-- rel:strong -->
- [overview](../architecture/overview.md) <!-- rel:strong -->
