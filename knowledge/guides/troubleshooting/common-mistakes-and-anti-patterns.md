---
category: guides
subcategory: troubleshooting
confidence: low
documentType: how-to
scope: org
contentHash: 9bdeab91996d
tags: [anti-pattern, troubleshooting, faq]
source: (synthesized)
verified: 2026-07-16
synthetic: synthesized-faq
---

## Common Mistakes and Anti-Patterns

<!-- sdd-knowledge-synthesized -->

> Auto-generated from anti-patterns found across the knowledge base.

### Architecture

**From [`routerEngine` — Central HTTP Router](../../architecture/routerengine-central-http-router.md):**
1. **`logger.SetLogger`** — zerolog request logger (skips health and metrics URIs to avoid noise)
2. **`gin.Recovery`** — panic recovery → 500 response
3. **`VersionMiddleware`** — injects server version header

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

**From [Security — API Keys and Credentials](../../security/security-api-keys-and-credentials.md):**
Gorush handles several categories of secrets for push delivery. All secrets are passed via config YAML or environment variables — never hardcoded.

