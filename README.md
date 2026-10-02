# Proxima Desktop Agent Hub and MCP Bridge

> An Electron desktop app paired with a local Model Context Protocol server. The MCP process bridges coding tools to the desktop Agent Hub over loopback IPC.

**Status:** Source repository inspected; desktop startup, builds, provider compatibility, and end-to-end tool calls were not verified in this documentation update.

The repository name says multi-LLM gateway, while its package metadata describes a local MCP server and its source contains Electron provider engines plus a loopback bridge. This README documents the checked-in implementation footprint, not a hosted OpenAI-compatible API, provider fallback service, or production gateway.

## What is included

| Part | Path | Verified from source tree |
|---|---|---|
| Electron desktop app | `electron/` | Main process, UI, IPC/WebSocket bridge, and provider engine files |
| MCP stdio server | `src/mcp-server-v3.js` | MCP server connects to `127.0.0.1`; default IPC port is `19222`, override with `AGENT_HUB_PORT` |
| CLI | `cli/proxima-cli.cjs` | Entry file exists; behavior not tested |
| JavaScript and Python SDK files | `sdk/` | Source files exist; package compatibility not tested |
| Provider engines | `electron/providers/` | Files exist for ChatGPT, Claude, Gemini, and Perplexity |

The provider engine files and their presence do not establish current provider compatibility or support guarantees.

## Local start

Requires a compatible Node.js/npm installation. Exact supported versions are not declared in the checked package metadata.

```sh
npm install
npm start
```

The root package defines `start` as `electron .`. This command was not run here.

To start the MCP server:

```sh
npm run mcp
```

The MCP server uses stdio and expects the desktop Agent Hub to be reachable on loopback at port `19222` by default. These commands are documented by package scripts and source code, not runtime-validated.

## Configuration and data flow

- The MCP bridge can use `AGENT_HUB_PORT` to select its local IPC port.
- Provider engines run through Electron browser views. Requests may be sent to the corresponding third-party provider using the user's session.
- This repository does not establish that prompts stay on-device or that provider accounts handle data in a particular way.
- Do not send sensitive prompts or connect accounts until you review the source, provider terms, and current data flow.
- Keep browser sessions, credentials, and tokens out of logs, issue reports, and version control.

## Claims and limits

Earlier README language described an OpenAI-compatible multi-provider gateway with automatic fallback, cost caps, and per-key rate limits. Those claims were not supported by the package metadata and source paths inspected for this update, so they are not repeated as verified capabilities.

No provider integration test, benchmark, privacy review, security audit, release build, or production deployment was run or established here.

## Documentation

- [Documentation and control index](docs/README.md)
- [MCP server source](src/mcp-server-v3.js)
- [Electron application](electron/)
- [Provider engines](electron/providers/)
- [Personal Use License](LICENSE)

- [Security and data handling](SECURITY.md)

## License

The checked-in [license](LICENSE) permits personal, non-commercial use only and restricts commercial and enterprise use. Read the license text before using or distributing this software.