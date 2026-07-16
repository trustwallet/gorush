---
category: architecture
subcategory: infrastructure
confidence: low
documentType: explanation
scope: org
contentHash: 925032b0b097
tags: [service]
source: README.md
verified: 2026-07-16
---

## Quick Start

Create namespace as `gorush` as `gorush` and then your configuration map:

```sh
kubectl create -f k8s/gorush-namespace.yaml
kubectl create -f k8s/gorush-configmap.yaml
```

Create redis service:

```sh
kubectl create -f k8s/gorush-redis-deployment.yaml
kubectl create -f k8s/gorush-redis-service.yaml
```

Create gorush deployment controller provides declarative updates for Pods and ReplicaSets:

```sh
kubectl create -f k8s/gorush-deployment.yaml
```

## See Also
- [deploy gorush application](../../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:strong -->
- [run gorush in aws lambda](../../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:strong -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:related -->
- [basic usage](../../ci/workflows/basic-usage.md) <!-- rel:related -->
