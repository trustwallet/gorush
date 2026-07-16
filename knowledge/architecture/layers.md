# Architectural Layers

<!-- sdd-knowledge-generated -->

> Layer of each module (path/role-derived) and any calls that flow **up** the stack — a layering violation. Allowed flow: ui → controller → service → repository → model.

## Layer distribution

| Layer | Symbols |
|-------|---------|
| controller | 10 |
| model | 9 |

## Violations (0)

_No upward-flowing calls detected._

## See Also
- [router](../features/router.md) <!-- rel:strong -->
- [rpc](../features/rpc.md) <!-- rel:strong -->
- [logx](../features/logx.md) <!-- rel:strong -->
- [core](../libs/core.md) <!-- rel:strong -->
- [notify](../features/notify.md) <!-- rel:strong -->
