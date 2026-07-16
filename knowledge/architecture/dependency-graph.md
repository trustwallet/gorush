# Dependency Graph

<!-- sdd-knowledge-generated -->

## Feature Dependencies

```mermaid
flowchart LR
  _root --> config
  _root --> core
  _root --> status
  logx --> core
  logx --> config
  metric --> status
  notify --> config
  notify --> status
  notify --> core
  router --> config
  router --> core
  router --> status
  rpc --> config
  rpc --> core
  status --> config
  status --> storage
  storage --> config
```

## External Dependencies

| Package | Import Count |
|---------|--------------|
| `github.com` | 71 |
| `google.golang.org` | 12 |
| `golang.org` | 4 |
| `google-protobuf` | 3 |
| `grpc` | 2 |

