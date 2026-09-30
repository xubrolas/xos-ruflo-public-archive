# FULL_LOCAL_CODEX

Baseline: `ruvnet/ruflo@v3.48.0` / `bd42d873b0333d3ab7dbcc85c9beb601ef944bd3`

## Principle

```text
FULL ENABLED != FULL AUTHORIZED
XOS configures.
Ruflo operates.
Codex hosts/executes.
Human decides.
```

## Active project profile

The branch root `claude-flow.config.json` uses Ruflo's native configuration loader and passthrough daemon settings.

The branch `.agents/config.toml` configures Codex for bounded autonomy:

```text
approval_policy = never
sandbox_mode = workspace-write
web_search = disabled
network_access = false
policy.mode = enforce
swarm.automation.enabled = true
```

The only configured Ruflo MCP is a local stdio process:

```text
node v3/@claude-flow/cli/bin/mcp-server.js
```

No `npx`, registry lookup, or moving `@latest` is allowed in the master MCP path.

## Daemon

WorkerDaemon is enabled at the Ruflo capability/config level, but upstream AI workers remain fail-closed:

```text
daemon.aiWorkers.enabled = false
```

Reason: upstream `HeadlessWorkerExecutor` currently executes `claude --print`. The XOS target is to reuse the existing `@claude-flow/codex` execution implementation rather than create a parallel executor.

## External boundaries

The profile does not authorize implicit:

- external provider/API calls;
- PAYG/new spending;
- package/model download;
- moving `@latest`;
- external MCP exposure;
- merge/release/publish/deploy;
- scope expansion.

## Promotion

The branch is a candidate. Global Codex binding requires a deterministic build and minimal MCP boot/readback first. R001-R010 then run against the materialized runtime while dogfooding.
