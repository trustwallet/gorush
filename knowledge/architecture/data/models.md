# Data Models & Schemas

<!-- sdd-knowledge-generated -->

> Field-level shape of data models extracted via tree-sitter: TS interfaces / type aliases, Zod `z.object` schemas, Go/Rust/Swift structs, Kotlin data classes, and Python dataclasses. Scoped to domain data — UI views/props, view-models, design tokens (theme/style/colors), and constant/identifier namespaces are excluded. Deterministic, no LLM.

## Alert

_struct · `notify/notification.go`:41_

| Field | Type | Optional |
|-------|------|----------|
| `Action` | `string` | no |
| `ActionLocKey` | `string` | no |
| `Body` | `string` | no |
| `LaunchImage` | `string` | no |
| `LocArgs` | `[]string` | no |
| `LocKey` | `string` | no |
| `Title` | `string` | no |
| `Subtitle` | `string` | no |
| `TitleLocArgs` | `[]string` | no |
| `TitleLocKey` | `string` | no |
| `SummaryArg` | `string` | no |
| `SummaryArgCount` | `int` | no |

## AndroidStatus

_struct · `status/status.go`:37_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## AndroidStatus

_struct · `storage/memory/memory.go`:16_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## App

_struct · `status/status.go`:26_

| Field | Type | Optional |
|-------|------|----------|
| `Version` | `string` | no |
| `QueueMax` | `int` | no |
| `QueueUsage` | `int` | no |
| `TotalCount` | `int64` | no |
| `Ios` | `IosStatus` | no |
| `Android` | `AndroidStatus` | no |
| `Huawei` | `HuaweiStatus` | no |

## ConfYaml

_struct · `config/config.go`:115_

| Field | Type | Optional |
|-------|------|----------|
| `Core` | `SectionCore` | no |
| `API` | `SectionAPI` | no |
| `Android` | `SectionAndroid` | no |
| `Huawei` | `SectionHuawei` | no |
| `Ios` | `SectionIos` | no |
| `Queue` | `SectionQueue` | no |
| `Log` | `SectionLog` | no |
| `Stat` | `SectionStat` | no |
| `GRPC` | `SectionGRPC` | no |

## DefaultQueueLogger

_struct · `logx/log_interface.go`:18_

| Field | Type | Optional |
|-------|------|----------|
| `accessLogger` | `*logrus.Logger` | no |
| `errorLogger` | `*logrus.Logger` | no |

## healthClient

_struct · `rpc/client_grpc_health.go`:16_

| Field | Type | Optional |
|-------|------|----------|
| `client` | `proto.HealthClient` | no |
| `conn` | `*grpc.ClientConn` | no |

## HuaweiStatus

_struct · `status/status.go`:49_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## HuaweiStatus

_struct · `storage/memory/memory.go`:28_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## InputLog

_struct · `logx/log.go`:188_

| Field | Type | Optional |
|-------|------|----------|
| `ID` | `string` | no |
| `Status` | `string` | no |
| `Token` | `string` | no |
| `Message` | `string` | no |
| `Platform` | `int` | no |
| `Error` | `error` | no |
| `HideToken` | `bool` | no |
| `Format` | `string` | no |

## IosStatus

_struct · `status/status.go`:43_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## IosStatus

_struct · `storage/memory/memory.go`:22_

| Field | Type | Optional |
|-------|------|----------|
| `PushSuccess` | `int64` | no |
| `PushError` | `int64` | no |

## LogPushEntry

_struct · `logx/log.go`:25_

| Field | Type | Optional |
|-------|------|----------|
| `ID` | `string` | no |
| `Type` | `string` | no |
| `Platform` | `string` | no |
| `Token` | `string` | no |
| `Message` | `string` | no |
| `Error` | `string` | no |

## Metrics

_struct · `metric/metrics.go`:13_

| Field | Type | Optional |
|-------|------|----------|
| `TotalPushCount` | `*prometheus.Desc` | no |
| `IosSuccess` | `*prometheus.Desc` | no |
| `IosError` | `*prometheus.Desc` | no |
| `AndroidSuccess` | `*prometheus.Desc` | no |
| `AndroidError` | `*prometheus.Desc` | no |
| `HuaweiSuccess` | `*prometheus.Desc` | no |
| `HuaweiError` | `*prometheus.Desc` | no |
| `QueueUsage` | `*prometheus.Desc` | no |
| `GetQueueUsage` | `func() int` | no |

## PushNotification

_struct · `notify/notification.go`:67_

| Field | Type | Optional |
|-------|------|----------|
| `ID` | `string` | no |
| `Tokens` | `[]string` | no |
| `Platform` | `int` | no |
| `Message` | `string` | no |
| `Title` | `string` | no |
| `Image` | `string` | no |
| `Priority` | `string` | no |
| `ContentAvailable` | `bool` | no |
| `MutableContent` | `bool` | no |
| `Sound` | `interface{}` | no |
| `Data` | `D` | no |
| `Retry` | `int` | no |
| `APIKey` | `string` | no |
| `To` | `string` | no |
| `CollapseKey` | `string` | no |
| `DelayWhileIdle` | `bool` | no |
| `TimeToLive` | `*uint` | no |
| `RestrictedPackageName` | `string` | no |
| `DryRun` | `bool` | no |
| `Condition` | `string` | no |
| `Notification` | `*fcm.Notification` | no |
| `AppID` | `string` | no |
| `AppSecret` | `string` | no |
| `HuaweiNotification` | `*model.AndroidNotification` | no |
| `HuaweiData` | `string` | no |
| `HuaweiCollapseKey` | `int` | no |
| `HuaweiTTL` | `string` | no |
| `BiTag` | `string` | no |
| `FastAppTarget` | `int` | no |
| `Expiration` | `*int64` | no |
| `ApnsID` | `string` | no |
| `CollapseID` | `string` | no |
| `Topic` | `string` | no |
| `PushType` | `string` | no |
| `Badge` | `*int` | no |
| `Category` | `string` | no |
| `ThreadID` | `string` | no |
| `URLArgs` | `[]string` | no |
| `Alert` | `Alert` | no |
| `Production` | `bool` | no |
| `Development` | `bool` | no |
| `SoundName` | `string` | no |
| `SoundVolume` | `float32` | no |
| `Apns` | `D` | no |

## RequestPush

_struct · `notify/notification.go`:57_

| Field | Type | Optional |
|-------|------|----------|
| `Notifications` | `[]PushNotification` | no |

## ResponsePush

_struct · `notify/notification.go`:62_

| Field | Type | Optional |
|-------|------|----------|
| `Logs` | `[]logx.LogPushEntry` | no |

## SectionAndroid

_struct · `config/config.go`:169_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `APIKey` | `string` | no |
| `MaxRetry` | `int` | no |

## SectionAPI

_struct · `config/config.go`:158_

| Field | Type | Optional |
|-------|------|----------|
| `PushURI` | `string` | no |
| `StatGoURI` | `string` | no |
| `StatAppURI` | `string` | no |
| `ConfigURI` | `string` | no |
| `SysStatURI` | `string` | no |
| `MetricURI` | `string` | no |
| `HealthURI` | `string` | no |

## SectionAutoTLS

_struct · `config/config.go`:151_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `Folder` | `string` | no |
| `Host` | `string` | no |

## SectionBadgerDB

_struct · `config/config.go`:263_

| Field | Type | Optional |
|-------|------|----------|
| `Path` | `string` | no |

## SectionBoltDB

_struct · `config/config.go`:247_

| Field | Type | Optional |
|-------|------|----------|
| `Path` | `string` | no |
| `Bucket` | `string` | no |

## SectionBuntDB

_struct · `config/config.go`:253_

| Field | Type | Optional |
|-------|------|----------|
| `Path` | `string` | no |

## SectionCore

_struct · `config/config.go`:128_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `Address` | `string` | no |
| `ShutdownTimeout` | `int64` | no |
| `Port` | `string` | no |
| `MaxNotification` | `int64` | no |
| `WorkerNum` | `int64` | no |
| `QueueNum` | `int64` | no |
| `Mode` | `string` | no |
| `Sync` | `bool` | no |
| `SSL` | `bool` | no |
| `CertPath` | `string` | no |
| `KeyPath` | `string` | no |
| `CertBase64` | `string` | no |
| `KeyBase64` | `string` | no |
| `HTTPProxy` | `string` | no |
| `FeedbackURL` | `string` | no |
| `FeedbackTimeout` | `int64` | no |
| `PID` | `SectionPID` | no |
| `AutoTLS` | `SectionAutoTLS` | no |

## SectionGRPC

_struct · `config/config.go`:275_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `Port` | `string` | no |

## SectionHuawei

_struct · `config/config.go`:176_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `AppSecret` | `string` | no |
| `AppID` | `string` | no |
| `MaxRetry` | `int` | no |

## SectionIos

_struct · `config/config.go`:184_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `KeyPath` | `string` | no |
| `KeyBase64` | `string` | no |
| `KeyType` | `string` | no |
| `Password` | `string` | no |
| `Production` | `bool` | no |
| `MaxConcurrentPushes` | `uint` | no |
| `MaxRetry` | `int` | no |
| `KeyID` | `string` | no |
| `TeamID` | `string` | no |

## SectionLevelDB

_struct · `config/config.go`:258_

| Field | Type | Optional |
|-------|------|----------|
| `Path` | `string` | no |

## SectionLog

_struct · `config/config.go`:198_

| Field | Type | Optional |
|-------|------|----------|
| `Format` | `string` | no |
| `AccessLog` | `string` | no |
| `AccessLevel` | `string` | no |
| `ErrorLog` | `string` | no |
| `ErrorLevel` | `string` | no |
| `HideToken` | `bool` | no |

## SectionNATS

_struct · `config/config.go`:232_

| Field | Type | Optional |
|-------|------|----------|
| `Addr` | `string` | no |
| `Subj` | `string` | no |
| `Queue` | `string` | no |

## SectionNSQ

_struct · `config/config.go`:225_

| Field | Type | Optional |
|-------|------|----------|
| `Addr` | `string` | no |
| `Topic` | `string` | no |
| `Channel` | `string` | no |

## SectionPID

_struct · `config/config.go`:268_

| Field | Type | Optional |
|-------|------|----------|
| `Enabled` | `bool` | no |
| `Path` | `string` | no |
| `Override` | `bool` | no |

## SectionQueue

_struct · `config/config.go`:218_

| Field | Type | Optional |
|-------|------|----------|
| `Engine` | `string` | no |
| `NSQ` | `SectionNSQ` | no |
| `NATS` | `SectionNATS` | no |

## SectionRedis

_struct · `config/config.go`:239_

| Field | Type | Optional |
|-------|------|----------|
| `Addr` | `string` | no |
| `Username` | `string` | no |
| `Password` | `string` | no |
| `DB` | `int` | no |

## SectionStat

_struct · `config/config.go`:208_

| Field | Type | Optional |
|-------|------|----------|
| `Engine` | `string` | no |
| `Redis` | `SectionRedis` | no |
| `BoltDB` | `SectionBoltDB` | no |
| `BuntDB` | `SectionBuntDB` | no |
| `LevelDB` | `SectionLevelDB` | no |
| `BadgerDB` | `SectionBadgerDB` | no |

## Server

_struct · `rpc/server.go`:22_

| Field | Type | Optional |
|-------|------|----------|
| `cfg` | `*config.ConfYaml` | no |
| `mu` | `sync.Mutex` | no |
| `statusMap` | `map[string]proto.HealthCheckResponse_ServingStatus` | no |

## Sound

_struct · `notify/notification_apns.go`:48_

| Field | Type | Optional |
|-------|------|----------|
| `Critical` | `int` | no |
| `Name` | `string` | no |
| `Volume` | `float32` | no |

## statApp

_struct · `storage/memory/memory.go`:8_

| Field | Type | Optional |
|-------|------|----------|
| `TotalCount` | `int64` | no |
| `Ios` | `IosStatus` | no |
| `Android` | `AndroidStatus` | no |
| `Huawei` | `HuaweiStatus` | no |

## Storage

_struct · `storage/badger/badger.go`:22_

| Field | Type | Optional |
|-------|------|----------|
| `config` | `*config.ConfYaml` | no |
| `opts` | `badger.Options` | no |
| `name` | `string` | no |
| `db` | `*badger.DB` | no |

## Storage

_struct · `storage/boltdb/boltdb.go`:20_

| Field | Type | Optional |
|-------|------|----------|
| `config` | `*config.ConfYaml` | no |
| `db` | `*storm.DB` | no |

## Storage

_struct · `storage/buntdb/buntdb.go`:22_

| Field | Type | Optional |
|-------|------|----------|
| `config` | `*config.ConfYaml` | no |
| `db` | `*buntdb.DB` | no |

## Storage

_struct · `storage/leveldb/leveldb.go`:31_

| Field | Type | Optional |
|-------|------|----------|
| `config` | `*config.ConfYaml` | no |
| `db` | `*leveldb.DB` | no |

## Storage

_struct · `storage/memory/memory.go`:41_

| Field | Type | Optional |
|-------|------|----------|
| `stat` | `*statApp` | no |

## Storage

_struct · `storage/redis/redis.go`:26_

| Field | Type | Optional |
|-------|------|----------|
| `config` | `*config.ConfYaml` | no |
| `client` | `*redis.ClusterClient` | no |

