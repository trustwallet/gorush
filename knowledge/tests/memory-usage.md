---
category: tests
confidence: low
documentType: reference
scope: org
contentHash: b4d6a02a629b
tags: [test]
source: README.md
verified: 2026-07-16
---

## Memory Usage

Memory average usage: **28Mb** (the total bytes of memory obtained from the OS.)

![memory usage](screenshot/memory.png)

Test Command (We use [bat](https://github.com/astaxie/bat) as default cli tool.):

```sh
for i in {1..9999999}; do bat -b.N=1000 -b.C=100 POST localhost:8088/api/push notifications:=@notification.json; sleep 1;  done
```

## See Also
- [download a binary](../ci/download-a-binary.md) <!-- rel:strong -->
- [run gorush in docker](../ci/workflows/run-gorush-in-docker.md) <!-- rel:strong -->
- [features](../observability/alerting/features.md) <!-- rel:strong -->
- [get metrics](../observability/metrics/get-metrics.md) <!-- rel:strong -->
- [command usage](../ci/workflows/command-usage.md) <!-- rel:strong -->
