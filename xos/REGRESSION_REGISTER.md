# Regression Register R001-R010

All items are evaluated from the pinned v3.48.0 baseline. Historical XOS patches are evidence only; do not port them blindly.

| ID | Seam | Entry status | Required semantic proof |
|---|---|---|---|
| R001 | runCodexLoop completion | defect proven | no false completed on exhaustion/stale marker/non-zero exit |
| R002 | ToolOutputGuardrail ESM loader | defect proven | strict guardrail actually loads and scans |
| R003 | WorkerDaemon queue reentrancy | source defect strong | one dispatch produces exactly one execution |
| R004 | MCP subscription lifecycle | defect proven | unsubscribe removes registry listener and session bookkeeping |
| R005 | MCP failed-start cleanup | reprobe | no timers/resources survive failed start |
| R006 | MCP logging level validation | defect proven | invalid levels rejected without state mutation |
| R007 | Ruflo Core hook command mapping | defect proven | enabled hooks invoke real CLI semantics, not swallowed unknown commands |
| R008 | SONA native stats compatibility | reprobe | native stats parse without exception/false metrics |
| R009 | Codex execution wiring | wiring gap | Agent/Workflow/Daemon/Autopilot reuse existing Codex backend |
| R010 | moving latest/materialization | occurrences proven | active profile executes no @latest/implicit install/download |

## Evidence rules

```text
dispatch != completed work
exit 0 != semantic success
source exists != wired/qualified
role name != permission enforcement
technical access != authority
```

## Stages

1. SOURCE_PREFLIGHT — source/config inspection; cannot claim runtime PASS.
2. MATERIALIZED_RUNTIME — deterministic build identity/readback.
3. SEMANTIC_E2E — real execution and negative path.
4. PATCH — only smallest residual Ruflo-owned gap.
5. RE-RUN — prove regression fixed without hiding failure.
