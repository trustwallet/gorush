---
category: architecture
subcategory: data
confidence: low
documentType: explanation
scope: repo
contentHash: 62a7c8128349
tags: [metrics, prometheus]
source: architecture/data/models.md
verified: 2026-07-22
splitPartIndex: 2
splitPartTotal: 4
canonical: false
synthetic: split-part
---

## Data Models & Schemas (Part 2)

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
