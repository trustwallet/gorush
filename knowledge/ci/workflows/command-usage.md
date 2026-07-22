---
category: ci
subcategory: workflows
confidence: medium
documentType: how-to
scope: org
contentHash: e2109c2152a2
tags: [command]
source: README.md
verified: 2026-07-22
---

## Command Usage

```sh
  ________                              .__
 /  _____/   ____ _______  __ __  ______|  |__
/   \  ___  /  _ \\_  __ \|  |  \/  ___/|  |  \
\    \_\  \(  <_> )|  | \/|  |  /\___ \ |   Y  \
 \______  / \____/ |__|   |____//____  >|___|  /
        \/                           \/      \/

Usage: gorush [options]

Server Options:
    -A, --address <address>          Address to bind (default: any)
    -p, --port <port>                Use port for clients (default: 8088)
    -c, --config <file>              Configuration file path
    -m, --message <message>          Notification message
    -t, --token <token>              Notification token
    -e, --engine <engine>            Storage engine (memory, redis ...)
    --title <title>                  Notification title
    --proxy <proxy>                  Proxy URL (support http, https, or socks5)
    --pid <pid path>                 Process identifier path
    --redis-addr <redis addr>        Redis addr (default: localhost:6379)
iOS Options:
    -i, --key <file>                 certificate key file path
    -P, --password <password>        certificate key password
    --ios                            enabled iOS (default: false)
    --production                     iOS production mode (default: false)
Android Options:
    -k, --apikey <api_key>           Android API Key
    --android                        enabled android (default: false)
Huawei Options:
    -hk, --hmskey <hms_key>          HMS App Secret
    -hid, --hmsid <hms_id>           HMS App ID
    --huawei                         enabled huawei (default: false)
Common Options:
    --topic <topic>                  iOS or Android topic message
    -h, --help                       Show this message
    -V, --version                    Show version
```

## See Also
- [memory usage](../../tests/memory-usage.md) <!-- rel:strong -->
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:related -->
- [create the service controller for aws elb](../../architecture/infrastructure/create-the-service-controller-for-aws-elb.md) <!-- rel:related -->
- [ingress controller for aws alb](../../architecture/infrastructure/ingress-controller-for-aws-alb.md) <!-- rel:related -->
- [install from source](../../code-conventions/git/install-from-source.md) <!-- rel:related -->
