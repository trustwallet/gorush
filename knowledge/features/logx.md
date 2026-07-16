# Logx

<!-- sdd-knowledge-generated -->

## Overview

- **Files**: 3
- **Symbols**: 19
- **DTOs**: colorForPlatForm, typeForPlatForm

## Files

- `logx/log_interface.go` — QueueLogger, DefaultQueueLogger, Infof, Errorf, Fatalf, Info, Error, Fatal
- `logx/log_test.go`
- `logx/log.go` — LogPushEntry, init, InitLog, SetLogOut, SetLogLevel, colorForPlatForm, typeForPlatForm, hideToken, GetLogPushEntry, InputLog, LogPush

## Architecture

### Layers

**Dto**: `colorForPlatForm`, `typeForPlatForm`

**Other**: `LogPushEntry`, `init`, `InitLog`, `SetLogOut`, `SetLogLevel`, `hideToken`, `GetLogPushEntry`, `InputLog`, `LogPush`, `QueueLogger`, `DefaultQueueLogger`, `Infof`, `Errorf`, `Fatalf`, `Info`, `Error`, `Fatal`

## Class Diagram

```mermaid
classDiagram
  class LogPushEntry {
  }
  class InputLog {
  }
  class DefaultQueueLogger {
  }
```

## External Dependencies

- `github.com`

## Minimum Viable Specification

> Auto-generated specification for the **Logx** feature.

**Contracts**: colorForPlatForm, typeForPlatForm

**Key Types**: LogPushEntry, InputLog, DefaultQueueLogger

