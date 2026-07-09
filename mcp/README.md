# AESP MCP Integrations

> **Model Context Protocol (MCP) integrations for the Autonomous Engineering Specification.**

MCP is an open protocol that enables AI agents to interact with external tools, data sources, and services. This directory contains MCP server specifications, client configurations, and integration patterns for AESP-compliant agent swarms.

---

## What is MCP?

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io) is an open standard for connecting AI assistants to external data sources and tools. In AESP, MCP servers provide agents with:

- **Tool Access** — Execute commands, run queries, interact with APIs
- **Data Retrieval** — Query databases, read files, fetch metrics
- **Action Execution** — Create issues, trigger deployments, send notifications
- **Context Enrichment** — Access project documentation, coding standards, runbooks

---

## Available Integrations

### Example MCP Server
**File:** [`example-mcp-server.md`](example-mcp-server.md)

A complete guide to building an MCP server that integrates with AESP agent swarms. Covers:
- Server architecture and protocol implementation
- Tool definitions and schemas
- Authentication and authorization
- Error handling and logging
- Deployment patterns

**Use this as a starting point** for building your own MCP integrations.

---

## MCP Integration Patterns

### Pattern 1: Tool Provider
MCP server exposes tools that agents can invoke:

```
Agent -> MCP Client -> MCP Server -> External Tool/Service
```

Example: A GitHub MCP server that lets agents create PRs, add comments, and merge code.

### Pattern 2: Data Provider
MCP server provides data that agents can query:

```
Agent -> MCP Client -> MCP Server -> Database/API
```

Example: A monitoring MCP server that lets agents query metrics and check service health.

### Pattern 3: Hybrid
MCP server provides both tools and data:

```
Agent <-> MCP Client <-> MCP Server <-> External System
```

Example: A JIRA MCP server that lets agents read tickets (data) and create new ones (tool).

---

## Configuring MCP in AESP

Add MCP servers to your swarm configuration:

```yaml
agents:
  - id: "backend-dev-1"
    role: "backend-developer"
    mcp_servers:
      - name: "github"
        command: "npx -y @modelcontextprotocol/server-github"
        env:
          GITHUB_PERSONAL_ACCESS_TOKEN: "{{secrets.github_token}}"
      - name: "postgres"
        command: "npx -y @modelcontextprotocol/server-postgres"
        args: ["postgresql://localhost/mydb"]
```

---

## Security Considerations

- **Authentication**: All MCP connections must be authenticated
- **Authorization**: Tools should enforce RBAC based on agent roles
- **Audit Logging**: All MCP tool invocations are logged
- **Secrets Management**: Never hardcode credentials in MCP configs
- **Rate Limiting**: Protect external services from excessive calls
- **Input Validation**: Validate all parameters before execution

---

## Contributing MCP Integrations

See [CONTRIBUTING.md](../CONTRIBUTING.md). When contributing an MCP integration:

1. Document the tools and resources your server provides
2. Include authentication setup instructions
3. Provide example agent configurations
4. List tested model compatibility
5. Include error handling patterns

---

*Part of the [AESP Examples](../README.md) repository.*
