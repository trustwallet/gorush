---
category: build
confidence: medium
documentType: reference
scope: org
contentHash: 7b981b7a6c07
tags: [build]
source: README.md
verified: 2026-07-22
---

## Build gorush binary

Download source code first.

```sh
git clone https://github.com/appleboy/gorush.git
cd gorush && make build_linux_lambda
```

you can see the binary file in `release/linux/lambda/` folder

## See Also
- [deploy gorush application](../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [download a binary](../ci/download-a-binary.md) <!-- rel:strong -->
- [install from source](../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [run gorush in aws lambda](../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:weak -->
- [run gorush in docker](../ci/workflows/run-gorush-in-docker.md) <!-- rel:weak -->
