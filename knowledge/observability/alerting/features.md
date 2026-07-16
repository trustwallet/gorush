---
category: observability
subcategory: alerting
confidence: medium
documentType: reference
scope: org
contentHash: f94b5e7e97ff
tags: [metrics, prometheus]
source: README.md
verified: 2026-07-16
---

## Features

- Support [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) using [go-fcm](https://github.com/appleboy/go-fcm) library for Android.
- Support [HTTP/2](https://http2.github.io/) Apple Push Notification Service using [apns2](https://github.com/sideshow/apns2) library.
- Support [HMS Push Service](https://developer.huawei.com/consumer/en/hms/huawei-pushkit) using [go-hms-push](https://github.com/msalihkarakasli/go-hms-push) library for Huawei Devices.
- Support [YAML](https://github.com/go-yaml/yaml) configuration.
- Support command line to send single Android or iOS notification.
- Support Web API to send push notification.
- Support [HTTP/2](https://http2.github.io/) or HTTP/1.1 protocol.
- Support notification queue and multiple workers.
- Support `/api/stat/app` show notification success and failure counts.
- Support `/api/config` show your [YAML](https://en.wikipedia.org/wiki/YAML) config.
- Support store app stat to memory, [Redis](http://redis.io/), [BoltDB](https://github.com/boltdb/bolt), [BuntDB](https://github.com/tidwall/buntdb), [LevelDB](https://github.com/syndtr/goleveldb) or [BadgerDB](https://github.com/dgraph-io/badger).
- Support `p8`, `p12` or `pem` format of iOS certificate file.
- Support `/sys/stats` show response time, status code count, etc.
- Support for HTTP, HTTPS or SOCKS5 proxy.
- Support retry send notification if server response is fail.
- Support expose [prometheus](https://prometheus.io/) metrics.
- Support install TLS certificates from [Let's Encrypt](https://letsencrypt.org/) automatically.
- Support send notification through [RPC](https://en.wikipedia.org/wiki/Remote_procedure_call) protocol, we use [gRPC](https://grpc.io/) as default framework.
- Support running in Docker, [Kubernetes](https://kubernetes.io/) or [AWS Lambda](https://aws.amazon.com/lambda) ([Native Support in Golang](https://aws.amazon.com/blogs/compute/announcing-go-support-for-aws-lambda/))
- Support graceful shutdown that workers and queue have been sent to APNs/FCM before shutdown service.
- Support different Queue as backend like [NSQ](https://nsq.io/) or [NATS](https://nats.io/), defaut engine is local [Channel](https://tour.golang.org/concurrency/2).

See the default [YAML config example](config/testdata/config.yml):

[embedmd]:# (config/testdata/config.yml yaml)
```yaml
core:
  enabled: true # enable httpd server
  address: "" # ip address to bind (default: any)
  shutdown_timeout: 30 # default is 30 second
  port: "8088" # ignore this port number if auto_tls is enabled (listen 443).
  worker_num: 0 # default worker number is runtime.NumCPU()
  queue_num: 0 # default queue number is 8192
  max_notification: 100
  sync: false # set true if you need get error message from fail push notification in API response.
  feedback_hook_url: "" # set a hook url if you need get error message asynchronously from fail push notification in API response.
  feedback_timeout: 10 # default is 10 second
  mode: "release"
  ssl: false
  cert_path: "cert.pem"
  key_path: "key.pem"
  cert_base64: ""
  key_base64: ""
  http_proxy: ""
  pid:
    enabled: false
    path: "gorush.pid"
    override: true
  auto_tls:
    enabled: false # Automatically install TLS certificates from Let's Encrypt.
    folder: ".cache" # folder for storing TLS certificates
    host: "" # which domains the Let's Encrypt will attempt

grpc:
  enabled: false # enable gRPC server
  port: 9000

api:
  push_uri: "/api/push"
  stat_go_uri: "/api/stat/go"
  stat_app_uri: "/api/stat/app"
  config_uri: "/api/config"
  sys_stat_uri: "/sys/stats"
  metric_uri: "/metrics"
  health_uri: "/healthz"

android:
  enabled: true
  apikey: "YOUR_API_KEY"
  max_retry: 0 # resend fail notification, default value zero is disabled

huawei:
  enabled: false
  appsecret: "YOUR_APP_SECRET"
  appid: "YOUR_APP_ID"
  max_retry: 0 # resend fail notification, default value zero is disabled

queue:
  engine: "local" # support "local", "nsq" and "nats " default value is "local"
  nsq:
    addr: 127.0.0.1:4150
    topic: gorush
    channel: gorush
  nats:
    addr: 127.0.0.1:4222
    subj: gorush
    queue: gorush

ios:
  enabled: false
  key_path: "key.pem"
  key_base64: "" # load iOS key from base64 input
  key_type: "pem" # could be pem, p12 or p8 type
  password: "" # certificate password, default as empty string.
  production: false
  max_concurrent_pushes: 100 # just for push ios notification
  max_retry: 0 # resend fail notification, default value zero is disabled
  key_id: "" # KeyID from developer account (Certificates, Identifiers & Profiles -> Keys)
  team_id: "" # TeamID from developer account (View Account -> Membership)

log:
  format: "string" # string or json
  access_log: "stdout" # stdout: output to console, or define log path like "log/access_log"
  access_level: "debug"
  error_log: "stderr" # stderr: output to console, or define log path like "log/error_log"
  error_level: "error"
  hide_token: true

stat:
  engine: "memory" # support memory, redis, boltdb, buntdb or leveldb
  redis:
    addr: "localhost:6379"
    password: ""
    db: 0
  boltdb:
    path: "bolt.db"
    bucket: "gorush"
  buntdb:
    path: "bunt.db"
  leveldb:
    path: "level.db"
  badgerdb:
    path: "badger.db"
```

## See Also
- [support platform](../../libs/support-platform.md) <!-- rel:strong -->
- [run gorush in aws lambda](../../ci/workflows/run-gorush-in-aws-lambda.md) <!-- rel:strong -->
- [send android notification](../../patterns/brand/voice/send-android-notification.md) <!-- rel:strong -->
- [android notification payload](../../patterns/brand/voice/android-notification-payload.md) <!-- rel:strong -->
- [run grpc service](../../tests/run-grpc-service.md) <!-- rel:strong -->
