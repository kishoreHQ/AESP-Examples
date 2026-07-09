# Project Specification Template

> **Template for writing an AESP-compliant project specification.**
>
> **AESP Reference:** AESP-0015 (Project Specification)
>
> A project specification defines the scope, goals, agent configuration,
> and delivery plan for an AESP-powered engineering project.

---

## Instructions

1. Replace all `[REPLACE: ...]` placeholders with your project-specific values
2. Remove example sections marked with `<!-- EXAMPLE -->` comments
3. Have the specification reviewed by stakeholders before starting work

---

## 1. Project Overview

```yaml
project:
  id: "[REPLACE: unique-project-identifier]"
  name: "[REPLACE: Human-readable Project Name]"
  version: "1.0.0"
  spec_version: "0.1.0"
  status: "[REPLACE: draft|review|approved|active|completed]"

  description: |
    [REPLACE: 3-5 paragraph description of the project:
     - What problem does it solve?
     - Who are the users/stakeholders?
     - What is the expected outcome?
     - What constraints or assumptions apply?]

  objectives:
    primary:
      - "[REPLACE: Main objective 1 with measurable success criteria]"
      - "[REPLACE: Main objective 2]"
    secondary:
      - "[REPLACE: Secondary objective 1]"
      - "[REPLACE: Secondary objective 2]"

  success_criteria:
    - metric: "[REPLACE: measurable criterion]"
      target: "[REPLACE: target value]"
      measurement_method: "[REPLACE: how it will be measured]"
```

---

## 2. Scope

### In Scope

```yaml
scope:
  in_scope:
    - "[REPLACE: deliverable or activity that IS included]"
    - "[REPLACE: another in-scope item]"
```

### Out of Scope

```yaml
  out_of_scope:
    - "[REPLACE: explicitly excluded item]"
    - "[REPLACE: another excluded item]"
    ## Clearly defining out-of-scope items prevents scope creep
    ## and sets stakeholder expectations
```

### Constraints

```yaml
  constraints:
    - type: "[REPLACE: technical|budget|timeline|resource|compliance]"
      description: "[REPLACE: constraint description]"
      impact: "[REPLACE: how this affects the project]"
```

---

## 3. Stakeholders

```yaml
stakeholders:
  - name: "[REPLACE: stakeholder name or role]"
    type: "[REPLACE: internal|external|customer|vendor]"
    responsibility: "[REPLACE: their role in the project]"
    communication_preference: "[REPLACE: how to communicate with them]"
```

---

## 4. Agent Team Configuration

### 4.1 Required Agent Roles

```yaml
agent_team:
  ## List all agent roles needed for this project
  roles:
    - role_id: "[REPLACE: role identifier]"
      role_name: "[REPLACE: human-readable name]"
      count: [REPLACE: number of agents with this role, e.g., 1]
      justification: "[REPLACE: why this role is needed]"
      autonomy_level: "[REPLACE: supervised|semi-autonomous|autonomous]"
      ## Reference to agent role definition
      role_definition: "[REPLACE: path/to/role-definition.yaml]"
```

### 4.2 Swarm Topology

```yaml
  ## Define how agents will collaborate
  swarm_topology:
    type: "[REPLACE: mesh|hub-spoke|pipeline|star|custom]"
    description: |
      [REPLACE: Explain why this topology was chosen and
       how agents will interact.]
    ## Reference to swarm configuration
    config: "[REPLACE: path/to/swarm-config.yaml]"
```

### 4.3 Communication Plan

```yaml
  communication:
    ## Communication channels and protocols
    channels:
      - name: "[REPLACE: channel name]"
        type: "[REPLACE: sync|async]"
        protocol: "[REPLACE: message|stream|rpc|email]"
        participants: ["[REPLACE: agent or stakeholder ids]"]
        purpose: "[REPLACE: what this channel is used for]"

    ## Meeting cadence (if applicable)
    meetings:
      - name: "[REPLACE: meeting name]"
        frequency: "[REPLACE: daily|weekly|biweekly|on-demand]"
        participants: ["[REPLACE: participant ids]"]
        purpose: "[REPLACE: meeting purpose]"
```

---

## 5. Workflows

```yaml
workflows:
  ## Define the workflows this project will use
  - workflow_id: "[REPLACE: unique workflow id]"
    name: "[REPLACE: human-readable name]"
    description: "[REPLACE: what this workflow does]"
    trigger: "[REPLACE: manual|scheduled|event-driven]"
    ## Reference to workflow definition
    definition: "[REPLACE: path/to/workflow.yaml]"
    ## Agents involved
    agents: ["[REPLACE: agent role ids]"]
    ## Expected output
    output: "[REPLACE: what this workflow produces]"
```

---

## 6. Deliverables

```yaml
deliverables:
  - id: "[REPLACE: deliverable-id]"
    name: "[REPLACE: Deliverable Name]"
    description: "[REPLACE: detailed description]"
    format: "[REPLACE: code|documentation|configuration|model|report]"
    acceptance_criteria:
      - "[REPLACE: specific criterion that defines done]"
      - "[REPLACE: another criterion]"
    assigned_to: "[REPLACE: agent role id or stakeholder]"
    due_date: "[REPLACE: YYYY-MM-DD]"
    dependencies: ["[REPLACE: other deliverable ids this depends on]"]
```

---

## 7. Timeline & Milestones

```yaml
timeline:
  start_date: "[REPLACE: YYYY-MM-DD]"
  end_date: "[REPLACE: YYYY-MM-DD]"
  timezone: "[REPLACE: e.g., UTC]"

  milestones:
    - id: "[REPLACE: milestone-id]"
      name: "[REPLACE: Milestone Name]"
      description: "[REPLACE: what is achieved at this milestone]"
      target_date: "[REPLACE: YYYY-MM-DD]"
      deliverables: ["[REPLACE: deliverable ids]"]
      success_criteria: "[REPLACE: how we know this milestone is complete]"
```

---

## 8. Risk Assessment

```yaml
risks:
  - id: "[REPLACE: risk-id]"
    description: "[REPLACE: risk description]"
    likelihood: "[REPLACE: high|medium|low]"
    impact: "[REPLACE: high|medium|low]"
    mitigation: "[REPLACE: how to reduce likelihood or impact]"
    contingency: "[REPLACE: what to do if the risk materializes]"
    owner: "[REPLACE: who is responsible for monitoring this risk]"
```

---

## 9. Quality Assurance

```yaml
quality_assurance:
  ## Quality standards to maintain
  standards:
    - "[REPLACE: applicable standard or guideline]"

  ## Review process
  review_process:
    - stage: "[REPLACE: review stage name]"
      reviewer: "[REPLACE: who reviews]"
      criteria: "[REPLACE: what is checked]"

  ## Testing strategy
  testing:
    - type: "[REPLACE: unit|integration|e2e|performance|security]"
      description: "[REPLACE: testing approach]"
      responsible: "[REPLACE: agent role responsible]"
```

---

## 10. Dependencies

```yaml
dependencies:
  ## External dependencies
  external:
    - name: "[REPLACE: dependency name]"
      type: "[REPLACE: service|library|api|team]"
      description: "[REPLACE: what it provides]"
      contact: "[REPLACE: who to contact]"
      sla: "[REPLACE: expected availability/response time]"

  ## Internal dependencies
  internal:
    - name: "[REPLACE: dependency name]"
      description: "[REPLACE: what it provides]"
      status: "[REPLACE: available|in-development|planned]"
```

---

## 11. Governance & Compliance

```yaml
governance:
  ## Decision-making authority
  decision_authority:
    - scope: "[REPLACE: what decisions]"
      authority: "[REPLACE: who decides]"
      escalation: "[REPLACE: escalation path]"

  ## Compliance requirements
  compliance:
    - requirement: "[REPLACE: compliance requirement]"
      standard: "[REPLACE: applicable standard]"
      verification: "[REPLACE: how compliance is verified]"

  ## Audit requirements
  audit:
    - type: "[REPLACE: audit type]"
      frequency: "[REPLACE: how often]"
      responsible: "[REPLACE: who performs it]"
```

---

## 12. Change Management

```yaml
change_management:
  ## How changes to this specification are handled
  process:
    - "Proposed changes are submitted as specification amendments"
    - "Changes are reviewed by project stakeholders"
    - "Approved changes are versioned and communicated"

  ## Version history
  history:
    - version: "1.0.0"
      date: "[REPLACE: YYYY-MM-DD]"
      author: "[REPLACE: author name]"
      changes: "[REPLACE: initial version]"
```

---

<!-- EXAMPLE START: Sample Project -->
## Example: E-Commerce API Project

Below is a filled-out example for building an e-commerce API using AESP.

```yaml
project:
  id: "ecommerce-api-v2"
  name: "E-Commerce API v2"
  version: "1.0.0"
  spec_version: "0.1.0"
  status: "draft"

  description: |
    Build a new REST API for the e-commerce platform to replace the
    legacy v1 API. The new API will support product catalog, inventory
    management, order processing, and payment integration. It will be
    built using microservices architecture with containerized deployment.

    Key stakeholders include the mobile app team, web frontend team,
    and third-party marketplace integrators.

  objectives:
    primary:
      - "Deliver REST API with 99.9% uptime SLA"
      - "Process 10,000 orders per minute at peak load"
      - "Reduce API response time P95 to < 100ms"
    secondary:
      - "Achieve 80% test coverage across all services"
      - "Complete security audit with zero critical findings"
      - "Document all public APIs with OpenAPI 3.0 specs"

  success_criteria:
    - metric: "API uptime"
      target: "> 99.9%"
      measurement_method: "Cloud monitoring dashboard"
    - metric: "Peak order throughput"
      target: ">= 10,000/min"
      measurement_method: "Load testing with k6"
    - metric: "Response time P95"
      target: "< 100ms"
      measurement_method: "APM metrics"

scope:
  in_scope:
    - "Product catalog API (CRUD, search, filtering)"
    - "Inventory management API"
    - "Order processing workflow"
    - "Payment gateway integration (Stripe, PayPal)"
    - "API documentation and developer portal"
    - "Deployment pipeline and infrastructure"
  out_of_scope:
    - "Mobile app development (separate project)"
    - "Web frontend (separate project)"
    - "Data analytics and reporting platform"
    - "Customer support chat system"
  constraints:
    - type: "budget"
      description: "Maximum cloud infrastructure cost $5,000/month"
      impact: "Must optimize resource usage and use auto-scaling"
    - type: "timeline"
      description: "Must launch before Black Friday (Nov 25)"
      impact: "6-month development window with hard deadline"
    - type: "compliance"
      description: "Must pass PCI-DSS audit for payment processing"
      impact: "Additional security requirements and documentation"

stakeholders:
  - name: "Mobile App Team"
    type: "internal"
    responsibility: "Primary API consumer for iOS/Android apps"
    communication_preference: "Slack #mobile-team, weekly sync"
  - name: "Marketplace Partners"
    type: "external"
    responsibility: "Third-party integrators using our API"
    communication_preference: "Email, quarterly reviews"
  - name: "CTO Office"
    type: "internal"
    responsibility: "Executive oversight and budget approval"
    communication_preference: "Monthly steering committee"

agent_team:
  roles:
    - role_id: "architect"
      role_name: "System Architect"
      count: 1
      justification: "Design microservices architecture and API contracts"
      autonomy_level: "semi-autonomous"
      role_definition: "templates/roles/architect.yaml"

    - role_id: "backend-dev"
      role_name: "Backend Developer"
      count: 2
      justification: "Implement microservices and business logic"
      autonomy_level: "semi-autonomous"
      role_definition: "templates/roles/backend-developer.yaml"

    - role_id: "code-reviewer"
      role_name: "Code Reviewer"
      count: 1
      justification: "Quality assurance for all code changes"
      autonomy_level: "semi-autonomous"
      role_definition: "templates/roles/code-reviewer.yaml"

    - role_id: "security-auditor"
      role_name: "Security Auditor"
      count: 1
      justification: "PCI-DSS compliance and security review"
      autonomy_level: "supervised"
      role_definition: "templates/roles/security-auditor.yaml"

    - role_id: "devops"
      role_name: "DevOps Engineer"
      count: 1
      justification: "CI/CD pipeline and infrastructure"
      autonomy_level: "autonomous"
      role_definition: "templates/roles/devops.yaml"

  swarm_topology:
    type: "hub-spoke"
    description: |
      The System Architect acts as the hub, coordinating all development
      activities. Backend developers report to the architect for design
      decisions. Code reviewer and security auditor review outputs.
      DevOps manages deployment independently.
    config: "swarm-config.yaml"

  communication:
    channels:
      - name: "dev-updates"
        type: "async"
        protocol: "message"
        participants: ["architect", "backend-dev", "code-reviewer"]
        purpose: "Daily development updates and blockers"
      - name: "security-reviews"
        type: "async"
        protocol: "message"
        participants: ["security-auditor", "architect"]
        purpose: "Security review requests and findings"
    meetings:
      - name: "Sprint Planning"
        frequency: "biweekly"
        participants: ["architect", "backend-dev"]
        purpose: "Plan upcoming sprint work"

workflows:
  - workflow_id: "feature-development"
    name: "Feature Development"
    description: "End-to-end feature development workflow"
    trigger: "event-driven"
    definition: "workflows/feature-development.yaml"
    agents: ["architect", "backend-dev", "code-reviewer"]
    output: "Production-ready code with tests"

  - workflow_id: "security-audit"
    name: "Security Audit"
    description: "Automated security scanning and review"
    trigger: "scheduled"
    definition: "workflows/security-audit.yaml"
    agents: ["security-auditor", "architect"]
    output: "Security report with findings and recommendations"

  - workflow_id: "ci-cd"
    name: "CI/CD Pipeline"
    description: "Build, test, and deploy pipeline"
    trigger: "event-driven"
    definition: "workflows/ci-cd.yaml"
    agents: ["devops", "code-reviewer"]
    output: "Deployed application in target environment"

deliverables:
  - id: "api-gateway"
    name: "API Gateway Service"
    description: "Kong API Gateway with rate limiting and auth"
    format: "code"
    acceptance_criteria:
      - "Handles 10,000 RPM with < 10ms overhead"
      - "JWT authentication implemented"
      - "Rate limiting per API key"
    assigned_to: "backend-dev"
    due_date: "2025-08-15"
    dependencies: []

  - id: "product-service"
    name: "Product Catalog Service"
    description: "Microservice for product CRUD and search"
    format: "code"
    acceptance_criteria:
      - "Full CRUD operations via REST"
      - "Elasticsearch integration for search"
      - "95% unit test coverage"
    assigned_to: "backend-dev"
    due_date: "2025-09-01"
    dependencies: ["api-gateway"]

  - id: "api-docs"
    name: "API Documentation"
    description: "OpenAPI 3.0 specs and developer portal"
    format: "documentation"
    acceptance_criteria:
      - "All endpoints documented with examples"
      - "Interactive docs hosted on developer portal"
      - "Changelog maintained"
    assigned_to: "architect"
    due_date: "2025-10-01"
    dependencies: ["product-service"]

timeline:
  start_date: "2025-06-01"
  end_date: "2025-11-20"
  timezone: "UTC"
  milestones:
    - id: "m1-architecture"
      name: "Architecture Complete"
      description: "All service designs and API contracts finalized"
      target_date: "2025-07-15"
      deliverables: ["api-gateway"]
      success_criteria: "Architecture review approved by CTO"

    - id: "m2-mvp"
      name: "MVP Release"
      description: "Core API services deployed to staging"
      target_date: "2025-09-15"
      deliverables: ["product-service"]
      success_criteria: "All MVP acceptance criteria passed"

    - id: "m3-production"
      name: "Production Launch"
      description: "Full API live in production"
      target_date: "2025-11-15"
      deliverables: ["api-docs"]
      success_criteria: "Production smoke tests passed, monitoring active"

risks:
  - id: "r1-performance"
    description: "API may not meet 10K orders/min target under load"
    likelihood: "medium"
    impact: "high"
    mitigation: "Implement load testing early; use caching and async processing"
    contingency: "Scale horizontally with auto-scaling groups"
    owner: "architect"

  - id: "r2-security"
    description: "PCI-DSS audit may reveal compliance gaps"
    likelihood: "medium"
    impact: "high"
    mitigation: "Engage security auditor early; follow secure coding practices"
    contingency: "Plan 2-week buffer before launch for remediation"
    owner: "security-auditor"

  - id: "r3-dependencies"
    description: "Payment gateway SDK changes may break integration"
    likelihood: "low"
    impact: "medium"
    mitigation: "Abstract payment layer; use adapter pattern"
    contingency: "Fallback to manual payment processing"
    owner: "backend-dev"
```
<!-- EXAMPLE END -->

---

## Validation Checklist

Before finalizing a project specification, verify:

- [ ] All placeholders replaced with project-specific values
- [ ] Objectives have measurable success criteria
- [ ] Scope is clearly defined with explicit out-of-scope items
- [ ] Agent team configuration covers all required roles
- [ ] Swarm topology is appropriate for the project type
- [ ] Deliverables have clear acceptance criteria
- [ ] Timeline is realistic with buffer for risks
- [ ] Risk assessment covers technical, schedule, and resource risks
- [ ] Dependencies are identified and tracked
- [ ] Change management process is defined

---

*Generated from AESP Project Specification Template v1.0.0*
