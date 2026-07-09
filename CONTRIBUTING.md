# Contributing to AESP Examples

Thank you for your interest in contributing to the AESP Examples repository! This document provides guidelines and instructions for contributing.

---

## Getting Started

1. **Read the Specification** — Familiarize yourself with the [Autonomous Engineering Specification](https://github.com/kishoreHQ/AESP) before contributing.
2. **Read the Code of Conduct** — All contributors must follow the [AESP Code of Conduct](https://github.com/kishoreHQ/AESP/blob/main/CODE_OF_CONDUCT.md).
3. **Fork and Clone** — Fork this repository and clone your fork locally.

```bash
git clone https://github.com/YOUR_USERNAME/AESP-Examples.git
cd AESP-Examples
```

---

## What Can I Contribute?

We welcome the following types of contributions:

### New Examples
- **Agent role implementations** — Real-world agent roles for specific domains (DevOps, data engineering, frontend, etc.)
- **Swarm configurations** — Example swarm topologies for common scenarios
- **Workflow definitions** — CI/CD, testing, deployment, incident response workflows
- **MCP server implementations** — Working MCP servers for popular tools and services
- **Project specifications** — Complete project specs following AESP-0015
- **System prompts** — Refined, tested system prompts for various agent roles

### Improvements to Existing Examples
- Bug fixes or corrections
- Clarity improvements to documentation
- Additional commentary explaining design decisions
- Cross-references to related AESP specifications

### New Categories
If you have an idea for a new example category not currently in the repository, please open an issue to discuss it first.

---

## Contribution Process

### 1. Check Existing Issues

Before starting work, check if an issue already exists for your contribution. If not, consider opening one to discuss your idea.

### 2. Create a Branch

```bash
git checkout -b examples/your-contribution-name
```

Use descriptive branch names:
- `examples/add-terraform-agent-role`
- `templates/improve-swarm-config`
- `prompts/add-ux-researcher-prompt`

### 3. Write Your Example

Follow these quality standards:

#### Content Requirements
- **Real, substantive content** — No placeholder text or lorem ipsum
- **Practical and usable** — Examples should work in real-world scenarios
- **Well-documented** — Every section must have explanatory comments
- **AESP-compliant** — Follow the current AESP specification
- **Vendor-neutral** — Avoid vendor-specific dependencies unless illustrating integration

#### Documentation Requirements
- Add a header comment explaining the example's purpose
- Include a "Prerequisites" section listing any dependencies
- Provide a "Usage" section showing how to use the example
- Add a "Customization" section explaining what can be modified

#### Formatting Standards
- Use clear, consistent formatting
- YAML files must be valid and linted
- Markdown files should render correctly on GitHub
- Follow the existing file structure and naming conventions

### 4. Test Your Example

Before submitting:
- Validate YAML files with a YAML linter
- Ensure all links in markdown files are correct
- Test any code snippets work as expected
- Review your example against the AESP specification for compliance

### 5. Submit a Pull Request

When you're ready, submit a pull request using our [PR template](.github/PULL_REQUEST_TEMPLATE.md).

Your PR should include:
- Clear description of what the example demonstrates
- Reference to relevant AESP specification sections
- Any dependencies or prerequisites
- Notes on testing performed

---

## Review Process

All contributions are reviewed by the **AESP Examples Committee**. The review process:

1. **Automated checks** — CI validates YAML syntax and link integrity
2. **Technical review** — Committee members review for accuracy and compliance
3. **Content review** — Ensures quality, clarity, and completeness
4. **Approval and merge** — Approved PRs are merged by maintainers

Reviews typically take 3-5 business days. We may request changes before merging.

---

## Commit Message Guidelines

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

Types:
- `docs` — Documentation changes
- `templates` — New or updated templates
- `prompts` — New or updated system prompts
- `workflows` — New or updated workflows
- `mcp` — MCP integration changes
- `projects` — Sample project changes
- `fix` — Bug fixes
- `chore` — Maintenance tasks

---

## Style Guide

### YAML Files
- Use 2 spaces for indentation
- Quote strings containing special characters
- Prefer explicit keys over inferred structures
- Include comments for complex sections

### Markdown Files
- Use ATX-style headers (`#` not underline)
- Use fenced code blocks with language specifiers
- Use reference-style links for repeated URLs
- Keep line length under 100 characters where practical

---

## Questions?

- Open a [GitHub Discussion](https://github.com/kishoreHQ/AESP-Examples/discussions)
- Join the AESP community chat (link in the main spec repo)

---

Thank you for contributing to the Autonomous Engineering Specification ecosystem!
