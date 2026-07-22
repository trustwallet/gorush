---
category: ci
subcategory: workflows
confidence: high
documentType: how-to
scope: org
contentHash: 990eaf80ce97
tags: [make , run ]
source: README.md
verified: 2026-07-22
---

## Run gorush web server

Please make sure your [config.yml](config/testdata/config.yml) exist. Default port is `8088`.

```bash
# for default config
$ gorush
# for custom config file
$ gorush -c config.yml
```

Get go status of api server using [httpie](https://github.com/jkbrzt/httpie) tool:

```bash
http -v --verify=no --json GET http://localhost:8088/api/stat/go
```

## See Also
- [features](../../observability/alerting/features.md) <!-- rel:strong -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:strong -->
- [install from source](../../code-conventions/git/install-from-source.md) <!-- rel:related -->
- [memory usage](../../tests/memory-usage.md) <!-- rel:related -->
- [without an aws account](../../build/without-an-aws-account.md) <!-- rel:related -->
