# Security

> Security guidelines, authentication, and compliance

## Sections

- [secrets/](secrets/index.md) — Secrets (security)

## Documents

| Document | Description | Source |
|----------|-------------|--------|
| [credential handling](credential-handling.md) | Credentials are loaded once at startup by `notify.InitAPNSClient`, `notify.InitFCMClient`, `notify.InitHMSClient`. | notify/notification_apns.go, notify/notification_fcm.go, config/config.go, logx/log.go |
| [ios example](ios-example.md) | Send normal notification. | README.md |

