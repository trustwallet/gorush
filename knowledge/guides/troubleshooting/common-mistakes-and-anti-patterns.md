---
category: guides
subcategory: troubleshooting
confidence: low
documentType: how-to
scope: org
contentHash: 34cf6b0d55ec
tags: [anti-pattern, troubleshooting, faq]
source: (synthesized)
verified: 2026-07-22
synthetic: synthesized-faq
---

## Common Mistakes and Anti-Patterns

<!-- sdd-knowledge-synthesized -->

> Auto-generated from anti-patterns found across the knowledge base.

### Architecture

**From [Queue Processing and Worker Lifecycle](../../architecture/queue-processing-and-worker-lifecycle.md):**
| Mode | Behaviour |
|------|-----------|
| `sync: false` (default) | `pushHandler` enqueues notifications and returns `200 OK` immediately with counts. Client never waits for actual delivery. |
| `sync: true` | A goroutine watches `c.Request.Context().Done()`. If the client disconnects, the context is cancelled, which stops in-progress `PushToIOS/Android/Huawei` calls. The handler returns only after all notifications finish. |

### Code-conventions

**From [Anti-Patterns (failed approaches)](../../code-conventions/anti-patterns-failed-approaches.md):**
<!-- Add failed approaches here. Each anti-pattern should include:
- **type**: anti-pattern
- **discovered**: YYYY-MM-DD

### Patterns

**From [Send Android notification](../../patterns/send-android-notification.md):**
- `--topic`: Send messages to topics. note: don't add device token.
- `--proxy`: Set `http`, `https` or `socks5` proxy url.

### Security

**From [Security: Credential Handling and Token Safety](../../security/security-credential-handling-and-token-safety.md):**
| Platform | Credential | How loaded |
|----------|------------|-----------|
| iOS/APNs | `.p8` private key OR `.p12`/`.pem` certificate | File path (`ios.key_path`) or base64 string (`ios.key_base64`) — never written to disk from base64 |
| Android/FCM | API Key | `android.apikey` config value |
| Huawei/HMS | App Secret + App ID | `huawei.appsecret` + `huawei.appid` config values |

