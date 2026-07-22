# Project Structure

<!-- sdd-knowledge-generated -->

## Languages

| Language | Files |
|----------|-------|
| Go | 50 |
| JavaScript | 3 |
| Ruby | 1 |
| **Total** | **54** |

## Directory Layout

```
├── HomebrewFormula/
│   └── gorush.rb
├── config/
│   ├── config.go
│   └── config_test.go
├── core/
│   ├── core.go
│   └── queue.go
├── doc.go
├── logx/
│   ├── log.go
│   ├── log_interface.go
│   └── log_test.go
├── main.go
├── metric/
│   ├── metrics.go
│   └── metrics_test.go
├── notify/
│   ├── feedback.go
│   ├── feedback_test.go
│   ├── global.go
│   ├── main_test.go
│   ├── notification.go
│   ├── notification_apns.go
│   ├── notification_apns_test.go
│   ├── notification_fcm.go
│   ├── notification_fcm_test.go
│   ├── notification_hms.go
│   ├── notification_hms_test.go
│   └── notification_test.go
├── router/
│   ├── server.go
│   ├── server_lambda.go
│   ├── server_normal.go
│   ├── server_test.go
│   └── version.go
├── rpc/
│   ├── client_grpc_health.go
│   ├── client_test.go
│   ├── example/
│   │   ├── go
│   │   └── node
│   ├── health.go
│   ├── server.go
│   └── server_test.go
├── status/
│   ├── status.go
│   └── status_test.go
└── storage/
    ├── badger/
    │   ├── badger.go
    │   └── badger_test.go
    ├── boltdb/
    │   ├── boltdb.go
    │   └── boltdb_test.go
    ├── buntdb/
    │   ├── buntdb.go
    │   └── buntdb_test.go
    ├── leveldb/
    │   ├── leveldb.go
    │   └── leveldb_test.go
    ├── memory/
    │   ├── memory.go
    │   └── memory_test.go
    ├── redis/
    │   ├── redis.go
    │   └── redis_test.go
    └── storage.go
```

## Features / Modules

| Feature | Files | Classes | Interfaces | Functions | Endpoints |
|---------|-------|---------|------------|-----------|----------|
| config | 2 | 19 | 0 | 1 | 0 |
| core | 2 | 0 | 0 | 1 | 0 |
| HomebrewFormula | 1 | 1 | 0 | 0 | 0 |
| logx | 3 | 3 | 0 | 10 | 0 |
| metric | 2 | 1 | 0 | 1 | 0 |
| notify | 12 | 5 | 0 | 21 | 0 |
| router | 5 | 0 | 0 | 23 | 2 |
| rpc | 10 | 2 | 1 | 14 | 0 |
| status | 2 | 4 | 0 | 1 | 0 |
| storage | 13 | 10 | 1 | 6 | 0 |

## Entry Points

- `main.go` (Go)
- `router/server.go` (Go)
- `rpc/example/go/health/main.go` (Go)
- `rpc/example/go/send/main.go` (Go)
- `rpc/server.go` (Go)

