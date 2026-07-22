---
category: code-conventions
subcategory: git
confidence: medium
documentType: tutorial
scope: org
contentHash: a8a6e4a73b58
tags: [git]
source: README.md
verified: 2026-07-22
---

## Install from source

#### Prerequisite Tools

- [Git](http://git-scm.com/)
- [Go (at least Go 1.11)](https://golang.org/dl/)

#### Fetch from GitHub

Gorush uses the Go Modules support built into Go 1.11 to build. The easiest way to get started is to clone Gorush in a directory outside of the GOPATH, as in the following example:

```sh
mkdir $HOME/src
cd $HOME/src
git clone https://github.com/appleboy/gorush.git
cd gorush
go install
```

## See Also
- [features](../../observability/alerting/features.md) <!-- rel:strong -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:strong -->
- [deploy gorush application](../../ci/deployment/deploy-gorush-application.md) <!-- rel:strong -->
- [run gorush in docker](../../ci/workflows/run-gorush-in-docker.md) <!-- rel:strong -->
- [ios example](../../security/ios-example.md) <!-- rel:strong -->
