---
category: architecture
subcategory: data
confidence: low
documentType: explanation
scope: org
contentHash: 9dc32178b9b1
tags: [observability, logging]
source: architecture/data/models.md
verified: 2026-07-16
splitPartIndex: 4
splitPartTotal: 4
canonical: false
synthetic: split-part
---

## Data Models & Schemas (Part 4)

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

## See Also
- [config schema](../../libs/config-schema.md) <!-- rel:strong -->
- [config](../../libs/config.md) <!-- rel:related -->
- [push logging](../../observability/push-logging.md) <!-- rel:weak -->
- [credentials](../../security/credentials.md) <!-- rel:weak -->
- [queue system](../../patterns/queue-system.md) <!-- rel:weak -->
