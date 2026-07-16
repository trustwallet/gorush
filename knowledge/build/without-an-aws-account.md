---
category: build
confidence: medium
documentType: reference
scope: org
contentHash: 256db1c9a2b1
tags: [build]
source: README.md
verified: 2026-07-16
---

## Without an AWS account

Or you can deploy gorush to alternative solution like [netlify functions](https://docs.netlify.com/functions/overview/). [Netlify](https://www.netlify.com/) lets you deploy serverless Lambda functions without an AWS account, and with function management handled directly within Netlify. Please see the netlify.toml file:

```toml
[build]
  command = "./build.sh"
  functions = "release/linux/lambda"

[build.environment]
  GO_IMPORT_PATH = "github.com/appleboy/gorush"
  GO111MODULE = "on"

[[redirects]]
  from = "/*"
  to = "/.netlify/functions/gorush/:splat"
  status = 200
```

## See Also
- [deploy gorush application](../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [run gorush in aws lambda](../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:related -->
- [support platform](../libs/support-platform.md) <!-- rel:related -->
- [features](../observability/alerting/features.md) <!-- rel:related -->
- [install from source](../code-conventions/git/install-from-source.md) <!-- rel:related -->
