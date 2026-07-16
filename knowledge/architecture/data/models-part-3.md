---
category: architecture
subcategory: data
confidence: low
documentType: explanation
scope: repo
contentHash: f7a2e6e4686a
tags: [architecture]
source: architecture/data/models.md
verified: 2026-07-16
splitPartIndex: 3
splitPartTotal: 4
canonical: false
synthetic: split-part
---

## Data Models & Schemas (Part 3)

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
