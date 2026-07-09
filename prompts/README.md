# AESP Prompt Library

> **Ready-to-use system prompts for AESP agent roles.**

System prompts define the behavior, capabilities, and constraints of AI agents in an AESP swarm. Each prompt in this library is designed to be dropped directly into a swarm configuration or used with your preferred AI model.

---

## Available Prompts

### Code Reviewer
**File:** [`system-prompts/code-reviewer.md`](system-prompts/code-reviewer.md)

A prompt for an agent that performs automated code reviews. Capabilities include:
- Static code analysis and bug detection
- Security vulnerability identification
- Performance optimization suggestions
- Style guide enforcement
- Educational feedback delivery

**Best for:** CI/CD pipelines, pre-merge checks, learning teams

---

### System Architect
**File:** [`system-prompts/architect.md`](system-prompts/architect.md)

A prompt for an agent that designs and validates software architecture. Capabilities include:
- System design and component decomposition
- Technology selection and evaluation
- API contract design
- Architecture decision records (ADRs)
- Non-functional requirements analysis

**Best for:** Greenfield projects, architecture reviews, technical planning

---

### Security Auditor
**File:** [`system-prompts/security-auditor.md`](system-prompts/security-auditor.md)

A prompt for an agent that performs security audits and compliance checks. Capabilities include:
- Vulnerability scanning and assessment
- Compliance validation (OWASP, PCI-DSS, SOC2)
- Secure coding practice review
- Threat modeling
- Security policy enforcement

**Best for:** Security reviews, compliance audits, pre-release checks

---

## Using Prompts

### In Swarm Configuration

Reference prompts in your swarm configuration file:

```yaml
agents:
  - id: "code-reviewer-1"
    config:
      system_prompt: "file://prompts/system-prompts/code-reviewer.md"
```

### Inline

Copy the prompt content directly into your agent configuration:

```yaml
agents:
  - id: "code-reviewer-1"
    config:
      system_prompt: |
        {{ paste prompt content here }}
```

### With Variables

Some prompts support variables for customization:

```yaml
agents:
  - id: "code-reviewer-1"
    config:
      system_prompt: |
        {{file://prompts/system-prompts/code-reviewer.md}}
        ## Custom Rules
        - Use {{project_language}} conventions
        - Follow {{team_name}} style guide
```

---

## Prompt Structure

Each prompt follows a consistent structure:

1. **Identity** — Who the agent is and its core purpose
2. **Capabilities** — What the agent can do, with specificity
3. **Process** — Step-by-step workflow the agent follows
4. **Output Format** — Structured output specification
5. **Constraints** — Explicit boundaries and limitations
6. **Escalation** — When and how to escalate

---

## Contributing Prompts

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines. When contributing a prompt:

1. Test the prompt with real code/documents
2. Include example inputs and outputs
3. Document any variables or customization points
4. Follow the standard prompt structure

---

*Part of the [AESP Examples](../README.md) repository.*
