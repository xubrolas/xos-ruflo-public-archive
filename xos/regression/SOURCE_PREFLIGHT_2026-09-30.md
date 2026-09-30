# SOURCE_PREFLIGHT — 2026-09-30

Branch: `xos/v3.48.0-full`

Baseline parent: `ruvnet/ruflo@v3.48.0`

Baseline commit: `bd42d873b0333d3ab7dbcc85c9beb601ef944bd3`

This is a source/config preflight only. It MUST NOT be cited as materialized-runtime or semantic E2E success/failure.

| ID | Source preflight | Evidence |
|---|---|---|
| R001 | DEFECT SIGNATURE CONFIRMED | completion marker is checked before non-zero exit; terminal fallback still maps non-stop exhaustion to `completed` |
| R002 | DEFECT SIGNATURE CONFIRMED | ESM CLI path uses `require('@claude-flow/security')` and catches loader failure open |
| R003 | SOURCE RISK CONFIRMED / E2E PENDING | 5s interval invokes async `processDispatchQueue()`; no `processingDispatchQueue` reentrancy guard |
| R004 | LIFECYCLE MISMATCH CONFIRMED | server tracks/deletes URI; ResourceRegistry unsubscribe API requires subscriptionId |
| R005 | SOURCE RISK CONFIRMED / E2E PENDING | `stop()` returns immediately when `running=false` |
| R006 | VALIDATION GAP CONFIRMED | logging level is cast to union without observed runtime membership validation |
| R007 | COMMAND MAPPING MISMATCH CONFIRMED | hook shim invokes `modify-bash` / `modify-file`; CLI command surface has neither |
| R008 | PARSER ASSUMPTION CONFIRMED / NATIVE E2E PENDING | SONA integration unconditionally `JSON.parse(statsJson)` |
| R009 | WIRING GAP CONFIRMED | Agent execution exposes Anthropic/OpenRouter/Ollama; Workflow uses that path; WorkerDaemon headless is Claude-oriented; `@claude-flow/codex` and `codex exec` already exist separately |
| R010 | MOVING/IMPLICIT PATHS CONFIRMED | `ruflo@latest` remains in Codex MCP config and DualMode memory flow; plugin has @latest fallback; performance manifest contains moving `latest` dependencies |

## Interpretation

```text
R001  patch candidate = confirmed
R002  patch candidate = confirmed
R003  do not patch until duplicate-execution E2E reproduces
R004  patch candidate = confirmed
R005  reproduce failed-start lifecycle before patch
R006  patch candidate = confirmed
R007  prefer remap to existing native hook commands before adding aliases
R008  reproduce real @ruvector/sona return shape before patch
R009  compose existing Ruflo Codex backend; do not create XOS executor
R010  classify every occurrence and patch/configure only executable active paths
```

## No semantic promotion from this document

This preflight does not prove:

- built package correctness;
- MCP startup;
- Task/Agent/Memory semantic behavior;
- WorkerDaemon duplicate execution;
- SONA native runtime failure;
- Codex worker wiring;
- global Codex configuration correctness.

Those require the deterministic materialized runtime.
