---
category: architecture
subcategory: data
confidence: low
documentType: explanation
scope: repo
contentHash: 626f6b182af2
tags: [architecture, domain]
source: architecture/data/models.md
verified: 2026-07-22
splitPartIndex: 1
splitPartTotal: 4
canonical: true
---

## Data Models & Schemas
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
