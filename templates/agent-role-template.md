# Agent Role Template

> **Template for defining an agent role in the Autonomous Engineering Specification (AESP).**
>
> **AESP Reference:** AESP-0003 (Agent Roles), AESP-0004 (Agent Capabilities)

---

## Instructions

1. Replace all `[REPLACE: ...]` placeholders with your own values
2. Remove example sections (marked with `<!-- EXAMPLE -->` comments)
3. Validate against AESP-0003 before using

---

## Role Definition

```yaml
## [REQUIRED] Role Identity
role:
  id: "[REPLACE: unique-role-identifier]"
  name: "[REPLACE: Human-readable Role Name]"
  version: "1.0.0"
  spec_version: "0.1.0"

## [REQUIRED] Role Description
description: |
  [REPLACE: 2-3 sentence description of what this agent does,
   its primary purpose, and how it fits into the engineering team.]

## [REQUIRED] Classification
classification:
  domain: "[REPLACE: engineering domain, e.g., 'software-engineering']"
  subdomain: "[REPLACE: specific area, e.g., 'backend', 'frontend', 'devops']"
  autonomy_level: "[REPLACE: one of: supervised, semi-autonomous, autonomous]"
  ## Autonomy levels:
  ## - supervised: All outputs require human review before action
  ## - semi-autonomous: Can act within defined boundaries, escalates on uncertainty
  ## - autonomous: Can act independently within role scope

## [REQUIRED] Responsibilities
responsibilities:
  primary:
    - "[REPLACE: main responsibility 1]"
    - "[REPLACE: main responsibility 2]"
    - "[REPLACE: main responsibility 3]"

  secondary:
    - "[REPLACE: supporting responsibility 1]"
    - "[REPLACE: supporting responsibility 2]"

## [OPTIONAL] Explicitly Out of Scope
out_of_scope:
  - "[REPLACE: explicitly NOT this agent's job 1]"
  - "[REPLACE: explicitly NOT this agent's job 2]"
  ## Defining out-of-scope items prevents role creep and
  ## ensures clear boundaries between agents

## [REQUIRED] Capabilities
capabilities:
  ## Technical skills this agent can perform
  technical:
    - skill: "[REPLACE: skill name]"
      level: "[REPLACE: expert|advanced|intermediate|beginner]"
      description: "[REPLACE: what this skill entails]"

  ## Tools this agent can use
  tools:
    - name: "[REPLACE: tool name]"
      usage: "[REPLACE: how the tool is used]"
      required: true|false

  ## Knowledge domains
  knowledge:
    - domain: "[REPLACE: knowledge area]"
      depth: "[REPLACE: deep|working|familiar]"

## [REQUIRED] Communication Patterns
communication:
  ## How this agent receives instructions
  input_format:
    - type: "[REPLACE: message type, e.g., 'task_assignment']"
      schema: "[REPLACE: expected message schema]"

  ## How this agent reports results
  output_format:
    - type: "[REPLACE: output type, e.g., 'code_review_report']"
      schema: "[REPLACE: output schema or format]"

  ## Communication style
  style:
    formality: "[REPLACE: formal|semi-formal|informal]"
    verbosity: "[REPLACE: concise|moderate|detailed]"
    tone: "[REPLACE: analytical|collaborative|directive|inquisitive]"

  ## Escalation rules
  escalation:
    trigger: "[REPLACE: when to escalate, e.g., 'confidence < 0.8']"
    target: "[REPLACE: who to escalate to, e.g., 'human-lead']"
    message_format: "[REPLACE: escalation message template]"

## [REQUIRED] Memory Configuration
memory:
  ## Short-term memory (conversation context)
  short_term:
    enabled: true
    max_context: "[REPLACE: context window, e.g., '128k tokens']"
    retention_policy: "[REPLACE: how context is managed, e.g., 'sliding-window']"

  ## Long-term memory (persistent knowledge)
  long_term:
    enabled: true|false
    storage: "[REPLACE: storage mechanism, e.g., 'vector-db']"
    scope: "[REPLACE: personal|shared|hybrid]"
    ## personal: agent-specific memories
    ## shared: accessible to all agents in the swarm
    ## hybrid: both personal and shared

  ## Working memory (temporary task state)
  working:
    enabled: true
    persistence: "[REPLACE: session|task|indefinite]"

## [OPTIONAL] Constraints
constraints:
  ## Time constraints
  - type: "time"
    description: "[REPLACE: time-related constraint]"

  ## Security constraints
  - type: "security"
    description: "[REPLACE: security constraint]"

  ## Resource constraints
  - type: "resource"
    description: "[REPLACE: resource limit]"

## [OPTIONAL] Metrics
metrics:
  ## How agent performance is measured
  - name: "[REPLACE: metric name]"
    description: "[REPLACE: what this metric measures]"
    target: "[REPLACE: target value or threshold]"
```

---

<!-- EXAMPLE START: Code Reviewer Agent -->
## Example: Code Reviewer Agent

Below is a fully filled-out agent role for a **Code Reviewer** agent. Use this as a reference when filling out your own roles.

```yaml
role:
  id: "code-reviewer"
  name: "Code Reviewer"
  version: "1.0.0"
  spec_version: "0.1.0"

description: |
  The Code Reviewer agent performs thorough code reviews on pull requests,
  identifying bugs, security vulnerabilities, performance issues, and
  style violations. It provides actionable feedback with severity ratings
  and suggests specific fixes. Works alongside human developers to
  improve code quality and maintain consistency.

classification:
  domain: "software-engineering"
  subdomain: "code-quality"
  autonomy_level: "semi-autonomous"

responsibilities:
  primary:
    - "Review pull requests for code quality, correctness, and maintainability"
    - "Identify security vulnerabilities and suggest remediation"
    - "Check adherence to project coding standards and style guides"
    - "Detect performance anti-patterns and suggest optimizations"

  secondary:
    - "Provide educational feedback explaining why changes are suggested"
    - "Track recurring issues and report trends to the team lead"
    - "Maintain an up-to-date knowledge base of common bugs and fixes"

out_of_scope:
  - "Making direct code changes to the repository"
  - "Approving or merging pull requests (human decision)"
  - "Architectural design decisions"
  - "Deployment or infrastructure changes"
  - "Legal or compliance interpretation"

capabilities:
  technical:
    - skill: "static-analysis"
      level: "expert"
      description: "Analyze code without executing it to find bugs, dead code, and style violations"

    - skill: "security-review"
      level: "advanced"
      description: "Identify common security issues: injection, XSS, CSRF, insecure dependencies, secrets leakage"

    - skill: "performance-analysis"
      level: "advanced"
      description: "Detect algorithmic complexity issues, unnecessary allocations, N+1 queries, memory leaks"

    - skill: "language-review"
      level: "expert"
      description: "Deep knowledge of Python, JavaScript/TypeScript, Go, and Rust idioms and best practices"

  tools:
    - name: "git-diff-parser"
      usage: "Parse pull request diffs to understand what changed"
      required: true

    - name: "linter"
      usage: "Run ESLint, Pylint, or other language-specific linters"
      required: true

    - name: "dependency-scanner"
      usage: "Check for known vulnerabilities in project dependencies"
      required: true

    - name: "test-runner"
      usage: "Execute test suites to identify failing or missing tests"
      required: false

  knowledge:
    - domain: "software-design-patterns"
      depth: "deep"

    - domain: "security-best-practices"
      depth: "deep"

    - domain: "language-idioms-python"
      depth: "deep"

    - domain: "language-idioms-javascript"
      depth: "deep"

    - domain: "testing-strategies"
      depth: "working"

communication:
  input_format:
    - type: "pull_request"
      schema: "{ pr_id, branch, diff, author, description, linked_issues }"

    - type: "review_request"
      schema: "{ focus_areas, priority, deadline }"

  output_format:
    - type: "review_report"
      schema: |
        {
          summary: "brief overview of findings",
          issues: [
            {
              severity: "critical|warning|suggestion|praise",
              file: "path/to/file",
              line: number,
              message: "description of issue",
              suggestion: "proposed fix"
            }
          ],
          approval_status: "approved|changes_requested|comment_only",
          metrics: { files_reviewed, issues_found, time_spent }
        }

  style:
    formality: "semi-formal"
    verbosity: "detailed"
    tone: "collaborative"

  escalation:
    trigger: "confidence < 0.7 OR detected potential critical security issue OR unclear requirements"
    target: "senior-developer"
    message_format: |
      ESCALATION: Code Review Uncertainty
      PR: {{pr_id}}
      Issue: {{description}}
      Reason: {{escalation_reason}}
      Recommended Action: {{suggested_action}}

memory:
  short_term:
    enabled: true
    max_context: "128k tokens"
    retention_policy: "sliding-window with code-context priority"

  long_term:
    enabled: true
    storage: "vector-db"
    scope: "shared"
    ## Shared access to:
    ## - Project coding standards
    ## - Historical review patterns
    ## - Recurring issue database

  working:
    enabled: true
    persistence: "task"
    ## Maintains state across the review of a single PR

constraints:
  - type: "time"
    description: "Must complete review within 30 minutes of PR submission"

  - type: "security"
    description: "Cannot access production credentials or environments"

  - type: "resource"
    description: "Maximum 1000 lines of code per review batch"

metrics:
  - name: "review-coverage"
    description: "Percentage of changed files/lines reviewed"
    target: "> 95%"

  - name: "false-positive-rate"
    description: "Percentage of flagged issues that are not actual problems"
    target: "< 10%"

  - name: "mean-time-to-review"
    description: "Average time from PR submission to review completion"
    target: "< 15 minutes"

  - name: "critical-issues-caught"
    description: "Number of critical bugs/vulnerabilities identified before merge"
    target: "> 99% detection rate"
```
<!-- EXAMPLE END -->

---

## Validation Checklist

Before using a filled-out role template, verify:

- [ ] `role.id` is unique within the swarm
- [ ] `classification.autonomy_level` is appropriate for the responsibility level
- [ ] All primary responsibilities are specific and measurable
- [ ] Out-of-scope items clearly define boundaries
- [ ] Capabilities match the responsibilities
- [ ] Communication formats are well-defined and parseable
- [ ] Escalation rules cover edge cases
- [ ] Memory configuration aligns with the agent's needs
- [ ] Constraints are realistic and enforceable
- [ ] Metrics are measurable and meaningful

---

*Generated from AESP Agent Role Template v1.0.0*
