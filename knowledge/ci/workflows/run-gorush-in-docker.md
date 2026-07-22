---
category: ci
subcategory: workflows
confidence: high
documentType: how-to
scope: repo
contentHash: d96e896dfb52
tags: [command, docker, run ]
source: README.md
verified: 2026-07-22
---

## Run gorush in Docker

Set up `gorush` in the cloud in under 5 minutes with zero knowledge of Golang or Linux shell using our [gorush Docker image](https://hub.docker.com/r/appleboy/gorush/).

```bash
docker pull appleboy/gorush
docker run --name gorush -p 80:8088 appleboy/gorush
```

Run `gorush` with your own config file.

```bash
docker pull appleboy/gorush
docker run --name gorush -v ${PWD}/config.yml:/config.yml -p 80:8088 appleboy/gorush
```

Testing your gorush server using [httpie](https://github.com/jkbrzt/httpie) command.

```bash
http -v --verify=no --json GET http://your.docker.host/api/stat/go
```

![statue screenshot](screenshot/status.png)

## See Also
- [features](../../observability/alerting/features.md) <!-- rel:strong -->
- [install from source](../../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:related -->
- [memory usage](../../tests/memory-usage.md) <!-- rel:related -->
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:related -->
