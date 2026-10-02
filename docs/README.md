# Documentation and control index

The repository is a local Electron Agent Hub paired with an MCP stdio bridge. The root README is the user-facing overview; source files are the canonical technical references.

## Start here

- [Project scope, commands, data flow, and limits](../README.md)
- [Personal Use License](../LICENSE)
- [Electron app entry and IPC bridge](../electron/main-v2.cjs)
- [MCP server](../src/mcp-server-v3.js)
- [Provider API bridge](../electron/provider-api.cjs)
- [Provider engines](../electron/providers/)
- [CLI entry](../cli/proxima-cli.cjs)
- [JavaScript SDK](../sdk/proxima.js)
- [Python SDK](../sdk/proxima.py)
- [Enabled providers example](../src/enabled-providers.example.json)

## Documentation gaps

[Security and data handling](../SECURITY.md) documents provider/session boundaries and review cautions. A supported-runtime matrix, provider compatibility matrix, user guide, release procedure, and vulnerability reporting instructions are not currently present. Do not infer these policies from the presence of source files or CI workflows. Add them when maintainers can provide accurate content and ownership.

## Verification boundary

The README commands come from the root package scripts and source configuration; they were not executed. Provider support, privacy behavior, release readiness, and security controls require separate validation.