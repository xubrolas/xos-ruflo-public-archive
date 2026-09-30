# MCP Entrypoint Contract

## Decision

There must be exactly one authoritative Ruflo MCP binding for the Codex profile.

```text
Codex App
   ⇅ MCP stdio
XOS-Ruflo persistent process
   ↓
native Ruflo tool registry/services
```

The canonical source entrypoint for this branch is:

```text
v3/@claude-flow/cli/bin/mcp-server.js
```

After deterministic build/materialization, the global Codex configuration must use an exact absolute path to the built XOS-Ruflo runtime. Relative path usage in this repository is only for project-local dogfooding.

## Forbidden master path

```text
npx ruflo@latest
npx @claude-flow/cli@latest
implicit registry lookup
plugin-contributed duplicate Ruflo MCP
```

## MCP policy

The existing upstream `.harness/mcp-policy.json` is preserved. Project-local MCP starts with `RUFLO_MCP_ENFORCE_POLICY=1`, so a missing/invalid policy fails closed.

This does not imply that every declarative policy field is enforced by the live MCP server. The current live enforcer is qualified separately.

## Runtime requirement

The source entrypoint imports built CLI artifacts from `dist/`. Therefore:

```text
source present != MCP materialized
```

A successful deterministic build plus process readback is mandatory before global promotion.
