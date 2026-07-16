---
title: "SCIP Go indexer requires go in PATH during KB Bootstrap"
date: 2026-07-16
pr: TBD
area: [kb-bootstrap, scip, go]
files: [steps/2.5-scip-index]
symptom: "scip-go not available — SCIP step silently falls through, AST path used"
tags: [scip, go, kb-bootstrap, gorush]
summary: "scip-go requires go in PATH; when Go is not installed in the container the SCIP index step falls through to the AST path, which is safe but loses member/dynamic call edge resolution."
---

# SCIP Go indexer requires `go` in PATH

## The Pattern

During KB Bootstrap step 2.5 for Go repos, the SCIP index generation uses `scip-go` which requires `go env GOPATH` to install and run. If the execution environment has no `go` binary (e.g. lightweight Node-only containers), the step silently falls through and `sdd-knowledge --full` uses AST-only path.

## The Rule

Always wrap `scip-go` in `|| true` (already done by the template). Never fail the bootstrap on SCIP unavailability. Verify the indexer is available with `which go` before the `go install` step to avoid a confusing non-zero exit. For gorush and other pure-Go repos on environments without Go, the AST heuristic path recovers ~133 member call edges via repo-wide unique name resolution, which is sufficient for most KB questions.

## Detection

If `knowledge/.relations.json` has edges with `via:"inferred"` (not `via:"scip"`), the SCIP index was not used. Check if `go` is in PATH: `command -v go`.

## Related

- KB Bootstrap step 2.5 in `templates/kb-bootstrap.md`
- `sdd-knowledge --full` `--INFERRED` log line in output
