# AESP Workflows

> **Workflow definitions for AESP-compliant agent swarms.**

Workflows define how agent teams execute tasks in a coordinated, repeatable manner. Each workflow specifies triggers, agent assignments, step sequences, and decision gates.

---

## Available Workflows

### CI/CD Pipeline
**File:** [`ci-cd-pipeline.yaml`](ci-cd-pipeline.yaml)

A complete continuous integration and deployment workflow using agent swarms.
Covers build, test, security scan, review, and deploy stages.

**Agents involved**: DevOps, Code Reviewer, Security Auditor
**Trigger**: Code push, pull request merge

---

### Code Review
**File:** [`code-review.yaml`](code-review.yaml)

An automated code review workflow that assigns reviewers, performs analysis,
and consolidates feedback.

**Agents involved**: Code Reviewer, Security Auditor, Architect
**Trigger**: Pull request creation/update

---

### Incident Response
**File:** [`incident-response.yaml`](incident-response.yaml)

A structured incident response workflow for handling production issues.
Covers detection, triage, mitigation, and post-incident review.

**Agents involved**: On-Call Engineer, Incident Commander, Communication Lead
**Trigger**: Alert threshold breach, manual trigger

---

## Workflow Format

All workflows follow the AESP Workflow Specification (AESP-0007):

```yaml
workflow:
  id: "unique-identifier"
  name: "Human-readable Name"
  version: "1.0.0"
  trigger: "event|schedule|manual"
  
  steps:
    - id: "step-1"
      name: "Step Name"
      agent: "agent-role"
      action: "what to do"
      output: "expected output"
      
    - id: "step-2"
      name: "Review Step"
      agent: "code-reviewer"
      input: "{{steps.step-1.output}}"
      gate: true  # Human approval required
```

## Using Workflows

1. Copy the workflow file to your project
2. Customize agent assignments and parameters
3. Integrate with your CI/CD platform or AESP runtime
4. Monitor execution and iterate

---

*Part of the [AESP Examples](../README.md) repository.*
