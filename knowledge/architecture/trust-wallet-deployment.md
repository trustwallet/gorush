---
title: Trust Wallet Deployment — gorush as Internal Push Gateway
category: architecture
tags: [deployment, trust-wallet, heroku, k8s, push-gateway]
confidence: high
source: knowledge from org KB, Dockerfile, .github/workflows/, k8s/, helm/
updated: 2026-07-16
---

# Trust Wallet Deployment

Trust Wallet forks and deploys gorush as an internal push notification gateway at `https://gorush.twinternal.net`.

## Deployment Topology

- **Primary hosting**: Heroku (via `deploy-heroku.yml` workflow using `akhileshns/heroku-deploy`)
- **Container registry**: AWS ECR (via `push-image.yml` workflow)
- **Kubernetes**: Helm chart in `helm/` + raw manifests in `k8s/`

## How Trust Wallet Uses It

| Consumer | Usage |
|----------|-------|
| `notification-manager-service` | Posts to gorush's `POST /api/push` with FCM/APNs tokens for transaction notifications, price alerts, and broadcast pushes |
| gRPC path | Low-latency delivery for select use cases |

## Payload at Trust Wallet

Trust Wallet adds structured `data` payloads to standard gorush notifications:

```json
{
  "notifications": [{
    "tokens": ["<device_token>"],
    "platform": 1,
    "message": "Your BTC arrived",
    "data": {
      "event": "transaction",
      "id": "0x553da0e27b...",
      "direction": "incoming"
    }
  }]
}
```

## Monitoring

Grafana dashboard: `https://monitoring.twinternal.net/d/z1WA0STGk/gorush`

Prometheus metrics are exposed at the path configured by `cfg.API.MetricURI` and scraped by the monitoring stack.

## Feedback Loop

`cfg.Core.FeedbackURL` is set to notification-manager-service's callback endpoint. Every push result (success or failure) is POSTed there for delivery tracking and retry decisions.

## See Also
- [architecture/overview.md](overview.md)
- [ci/deployment/deploy-gorush-application.md](../ci/deployment/deploy-gorush-application.md)
- [features](../observability/alerting/features.md) <!-- rel:strong -->
- [config schema](../libs/config-schema.md) <!-- rel:strong -->
- [credentials](../security/credentials.md) <!-- rel:strong -->
