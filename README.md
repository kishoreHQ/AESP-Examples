# AESP Examples — Templates, Prompts & Workflows

> **Example implementations, templates, prompts, workflows, MCP integrations, and sample projects for the [Autonomous Engineering Specification (AESP)](https://github.com/kishoreHQ/AESP).**

---

## Status

![AESP Version](https://img.shields.io/badge/AESP-v0.1.0--alpha-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active%20development-orange)

---

## What is AESP?

The **Autonomous Engineering Specification (AESP)** defines an open, vendor-neutral standard for building autonomous engineering teams powered by AI agents. It specifies:

- **Agent Roles** — standardized capabilities, responsibilities, and boundaries
- **Swarm Topologies** — how agents collaborate in structured teams
- **Communication Protocols** — message-passing, consensus, and conflict resolution
- **Memory & State Management** — short-term, long-term, and shared memory patterns
- **MCP Integration** — Model Context Protocol server specifications
- **Security & Governance** — audit trails, access control, and compliance

This repository contains **practical, ready-to-use examples** that demonstrate how to apply AESP in real-world projects.

---

## Repository Structure

```
AESP-Examples/
├── README.md                          # This file
├── LICENSE                            # MIT License
├── CONTRIBUTING.md                    # How to contribute examples
│
├── templates/                         # Reusable templates
│   ├── README.md                      # Templates index
│   ├── agent-role-template.md         # Define an agent role
│   ├── swarm-config-template.yaml     # Configure a multi-agent swarm
│   └── project-spec-template.md       # Write an AESP project specification
│
├── prompts/                           # System prompts library
│   ├── README.md                      # Prompts index
│   └── system-prompts/                # Ready-to-use system prompts
│       ├── code-reviewer.md
│       ├── architect.md
│       └── security-auditor.md
│
├── workflows/                         # Workflow definitions
│   ├── README.md                      # Workflows index
│   ├── ci-cd-pipeline.yaml            # CI/CD with agent swarms
│   ├── code-review.yaml               # Automated code review workflow
│   └── incident-response.yaml         # Incident response with agents
│
├── mcp/                               # MCP integrations
│   ├── README.md                      # MCP integrations index
│   └── example-mcp-server.md          # Build an MCP server for AESP
│
├── projects/                          # Sample projects
│   ├── README.md                      # Projects index
│   └── hello-aesp.md                  # "Hello World" getting started guide
│
└── .github/
    └── PULL_REQUEST_TEMPLATE.md       # PR template
```

---

## Quick Start

### 1. Clone This Repository

```bash
git clone https://github.com/kishoreHQ/AESP-Examples.git
cd AESP-Examples
```

### 2. Browse by Use Case

| I want to... | Go to... |
|---|---|
| Define a new agent role | [`templates/agent-role-template.md`](templates/agent-role-template.md) |
| Configure a multi-agent swarm | [`templates/swarm-config-template.yaml`](templates/swarm-config-template.yaml) |
| Set up a project following AESP | [`templates/project-spec-template.md`](templates/project-spec-template.md) |
| Use a ready-made system prompt | [`prompts/system-prompts/`](prompts/system-prompts/) |
| Implement CI/CD with agents | [`workflows/ci-cd-pipeline.yaml`](workflows/ci-cd-pipeline.yaml) |
| Build an MCP server | [`mcp/example-mcp-server.md`](mcp/example-mcp-server.md) |
| Get started from scratch | [`projects/hello-aesp.md`](projects/hello-aesp.md) |

### 3. Read the Specification

All examples in this repository are based on the [Autonomous Engineering Specification](https://github.com/kishoreHQ/AESP). Review the spec to understand the concepts behind each example.

### 4. Try the Reference Implementation

For a working runtime that implements AESP, see the [AESP Reference Implementation](https://github.com/kishoreHQ/AESP-Reference-Implementation).

---

## How to Use These Examples

### Using Templates

Templates are **copy-paste starting points**. Each template includes:

- **Commentary** explaining what each section does and why
- **Placeholder values** marked with `[REPLACE: ...]` or `{{placeholder}}`
- **Example fillings** showing realistic content

To use a template:

1. Copy the template file
2. Replace all placeholder values with your project-specific content
3. Remove the example fillings (or keep them as reference)
4. Validate against the AESP specification

### Using Prompts

System prompts in [`prompts/system-prompts/`](prompts/system-prompts/) are ready to drop into your agent configuration. Each prompt:

- Follows AESP agent role definitions
- Includes capability assertions
- Defines communication patterns
- Specifies output formats

```yaml
# Example: Using a prompt in a swarm config
agents:
  - name: code-reviewer
    role: code-reviewer
    system_prompt: |
      {{file://prompts/system-prompts/code-reviewer.md}}
```

### Using Workflows

Workflows are YAML definitions that can be loaded by an AESP-compliant runtime. They define:

- **Trigger conditions** — when the workflow activates
- **Agent assignments** — which agents participate
- **Step sequences** — ordered or parallel execution
- **Decision gates** — human-in-the-loop or automated checkpoints

### Using MCP Integrations

MCP (Model Context Protocol) integrations allow agents to interact with external tools, databases, and services. See [`mcp/`](mcp/) for server specifications and client configurations.

---

## Related Repositories

| Repository | Description |
|---|---|
| [kishoreHQ/AESP](https://github.com/kishoreHQ/AESP) | The core specification — defines standards, protocols, and formats |
| [kishoreHQ/AESP-Reference-Implementation](https://github.com/kishoreHQ/AESP-Reference-Implementation) | A working runtime that implements the AESP specification |
| **kishoreHQ/AESP-Examples** (this repo) | Practical examples, templates, and sample projects |

---

## Contributing

We welcome contributions! See [`CONTRIBUTING.md`](CONTRIBUTING.md) for guidelines on:

- Submitting new examples
- Improving existing templates
- Reporting issues with examples
- Suggesting new example categories

All contributions must follow the [AESP Code of Conduct](https://github.com/kishoreHQ/AESP/blob/main/CODE_OF_CONDUCT.md).

---

## License

This repository is licensed under the [MIT License](LICENSE).

Copyright (c) 2025 Kishore Kumar Behera and the AESP Contributors.

---

## Acknowledgments

These examples are built by the **AESP Examples Committee** as part of the Autonomous Engineering Standards initiative. Special thanks to all contributors who have provided real-world feedback and improvements.

---

*Part of the [Autonomous Engineering Specification](https://github.com/kishoreHQ/AESP) ecosystem.*
