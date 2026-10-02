# Security and data handling

## Scope and data flow

This repository contains a local Electron Agent Hub and MCP stdio bridge. Its provider engines can use the user's authenticated third-party provider session; prompts and context may therefore be processed by those providers. The loopback bridge and local desktop packaging do not establish that all data remains on-device or that same-user process access is isolated.

## Safe handling

- Do not enter sensitive prompts or connect provider accounts until the active provider, request content, logging, and retention behavior have been reviewed.
- Review the MCP server's registered tools and permissions before connecting a coding client. Grant only tools needed for the task.
- Keep browser sessions, cookies, credentials, and tokens out of source control, logs, screenshots, and issue reports.
- Treat provider names, availability, output handling, and policies as provider-controlled and time-sensitive.
- Review IPC/WebSocket exposure and local listener behavior before relying on the app in a multi-user or shared-host environment.

## Verification boundary

This document records checked-in source and configuration references. Desktop startup, provider requests, MCP tool execution, authentication, logging, and multi-user isolation were not runtime-tested for this documentation change. This is not a security certification.

Report vulnerabilities privately to the repository maintainer; do not publish session data or credentials.
