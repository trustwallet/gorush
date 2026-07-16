---
category: architecture
subcategory: infrastructure
confidence: low
documentType: explanation
scope: org
contentHash: cd73c0b57748
tags: [service]
source: README.md
verified: 2026-07-16
---

## Ingress Controller for AWS ALB

Update the following in `k8s/gorush-service.yaml`

```diff
-  type: LoadBalancer
-  # type: NodePort
+  # type: LoadBalancer
+  type: NodePort
```

Then start the AWS ALB by the follwong command.

```sh
kubectl create -f k8s/gorush-service.yaml
kubectl create -f k8s/gorush-aws-alb-ingress.yaml
```

## See Also
- [deploy gorush application](../../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:strong -->
- [send huawei hms notification](../../security/secrets/send-huawei-hms-notification.md) <!-- rel:strong -->
- [run gorush in aws lambda](../../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:strong -->
- [send android or ios notifications using firebase](../../ci/workflows/send-android-or-ios-notifications-using-firebase.md) <!-- rel:strong -->
