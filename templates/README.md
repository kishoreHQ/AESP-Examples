# AESP Templates

> **Reusable templates for building AESP-compliant autonomous engineering systems.**

These templates are starting points you can copy, customize, and use in your own projects. Each template includes detailed commentary and example fillings.

---

## Available Templates

### Agent Role Template
**File:** [`agent-role-template.md`](agent-role-template.md)

Define an agent role following the AESP agent specification. Includes:
- Role identity and purpose
- Responsibility boundaries
- Required capabilities
- Communication patterns
- Memory configuration
- Example: "Code Reviewer" agent

**When to use:** When creating a new agent role for your swarm.

---

### Swarm Configuration Template
**File:** [`swarm-config-template.yaml`](swarm-config-template.yaml)

Configure a multi-agent swarm with roles, topology, and workflows. Includes:
- Swarm metadata and version
- Agent definitions with role assignments
- Communication topology (mesh, hub-spoke, pipeline)
- Workflow assignments
- Shared memory configuration
- Health check definitions

**When to use:** When setting up a new swarm or modifying an existing one.

---

### Project Specification Template
**File:** [`project-spec-template.md`](project-spec-template.md)

Write a complete project specification following AESP-0015. Includes:
- Project overview and objectives
- Agent roles required
- Swarm topology design
- Workflow definitions
- Deliverables and acceptance criteria
- Timeline and milestones
- Risk assessment

**When to use:** When planning a new project that will use AESP agents.

---

## How to Use Templates

### 1. Copy the Template

```bash
cp templates/agent-role-template.md my-project/roles/backend-developer.md
```

### 2. Replace Placeholders

Templates use two placeholder conventions:

| Convention | Meaning | Example |
|---|---|---|
| `[REPLACE: description]` | Must be replaced with your value | `[REPLACE: agent role name]` |
| `{{placeholder}}` | Optional or contextual value | `{{project_name}}` |

### 3. Remove Example Content

Templates include **example fillings** showing realistic content. After replacing placeholders, remove the example sections (marked with `<!-- EXAMPLE START -->` and `<!-- EXAMPLE END -->` comments).

### 4. Validate

Before using your filled template, validate it against the AESP specification:

```bash
# Using the AESP CLI validator (from reference implementation)
aesp validate --template my-filled-template.yaml
```

---

## Template Conventions

### Comment Style
- `## ---` marks section boundaries
- `## [SECTION]` identifies template sections
- `# NOTE:` provides usage guidance
- `# EXAMPLE:` introduces example content

### Required vs. Optional
- Sections marked with `[REQUIRED]` must be filled
- Sections marked with `[OPTIONAL]` can be omitted if not applicable
- Fields with default values are shown in the template

### File Formats
- **Markdown (`.md`)** — For human-readable documents with rich formatting
- **YAML (`.yaml`)** — For machine-readable configurations
- **JSON (`.json`)** — For schemas and structured data (where applicable)

---

## Contributing New Templates

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines. When proposing a new template:

1. Open an issue describing the use case
2. Include a draft of the proposed template
3. Reference relevant AESP specification sections
4. Provide a real-world example of the template filled out

---

## Template Checklist

Before submitting a template, ensure:

- [ ] All placeholder values are clearly marked
- [ ] An example filling is provided
- [ ] Section comments explain purpose and usage
- [ ] Template follows AESP specification
- [ ] YAML validates (if applicable)
- [ ] Markdown renders correctly on GitHub
- [ ] Related AESP sections are referenced

---

*Part of the [AESP Examples](../README.md) repository.*
