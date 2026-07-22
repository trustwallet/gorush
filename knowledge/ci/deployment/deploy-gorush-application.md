---
category: ci
subcategory: deployment
confidence: medium
documentType: how-to
scope: org
contentHash: cf262b82fec4
tags: [deploy, release]
source: README.md
verified: 2026-07-22
---

## Deploy gorush application

we need to build a binary that will run on Linux, and ZIP it up into a deployment package.

```sh
zip deployment.zip release/linux/lambda/gorush
```

Upload the `deployment.zip` via web UI or you can try the [drone-lambda](https://github.com/appleboy/drone-lambda) as the following command. it will zip your binary file and upload to AWS Lambda automatically.

```sh
$ AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID \
  AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY \
  drone-lambda --region ap-southeast-1 \
  --function-name gorush \
  --source release/linux/lambda/gorush
```

## See Also
- [build gorush binary](../../build/build-gorush-binary.md) <!-- rel:strong -->
- [without an aws account](../../build/without-an-aws-account.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
- [install from source](../../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [ingress controller for aws alb](../../architecture/infrastructure/ingress-controller-for-aws-alb.md) <!-- rel:related -->
