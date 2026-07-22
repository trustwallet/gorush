---
category: architecture
subcategory: data
confidence: low
documentType: explanation
scope: org
contentHash: dad1ed3dd2eb
tags: [observability, alerting]
source: architecture/data/models.md
verified: 2026-07-22
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
- [config](../../libs/config.md) <!-- rel:strong -->
- [storage backends](../../observability/storage-backends.md) <!-- rel:strong -->
- [configuration](../../libs/configuration.md) <!-- rel:strong -->
- [features](../../observability/alerting/features.md) <!-- rel:related -->
- [credential handling](../../security/credential-handling.md) <!-- rel:related -->
