---
category: architecture
subcategory: infrastructure
confidence: medium
documentType: explanation
scope: org
contentHash: d86c71ddfea1
tags: [service]
source: README.md
verified: 2026-07-22
---

## Create the Service Controller for AWS ELB

```sh
kubectl create -f k8s/gorush-service.yaml
```

## See Also
- [run gorush in aws lambda](../../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:strong -->
- [deploy gorush application](../../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [without an aws account](../../build/without-an-aws-account.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:related -->
