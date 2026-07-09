# Hello AESP — Getting Started Guide

> **Your first steps with the Autonomous Engineering Specification.**
>
> **Complexity**: Beginner | **Time**: 15 minutes
>
> This guide walks you through creating your first AESP agent swarm and
> running a simple workflow. No prior experience with AESP required.

---

## What You'll Build

A minimal agent swarm with two agents:
- **Greeter Agent** — Says hello and introduces AESP
- **Echo Agent** — Echoes back messages with a twist

You'll learn:
1. How to define an agent role
2. How to configure a swarm
3. How to run a workflow
4. How agents communicate

---

## Prerequisites

- [ ] AESP CLI installed (`npm install -g @aesp/cli` or equivalent)
- [ ] An AI model API key (Anthropic, OpenAI, or local)
- [ ] Text editor (VS Code recommended with AESP extension)
- [ ] Terminal with `git` and `node` (v18+)

---

## Step 1: Create Project Directory

```bash
mkdir hello-aesp
cd hello-aesp
```

---

## Step 2: Define Agent Roles

Create `agent-roles/greeter.yaml`:

```yaml
# agent-roles/greeter.yaml
role:
  id: "greeter"
  name: "Greeter"
  version: "1.0.0"
  spec_version: "0.1.0"

description: |
  A friendly agent that welcomes users and explains AESP concepts
  in simple, approachable terms.

classification:
  domain: "education"
  subdomain: "onboarding"
  autonomy_level: "autonomous"

responsibilities:
  primary:
    - "Welcome new users to AESP"
    - "Explain basic concepts clearly"
    - "Guide users through their first workflow"

capabilities:
  technical:
    - skill: "communication"
      level: "expert"
      description: "Explain technical concepts in accessible language"

communication:
  style:
    formality: "informal"
    verbosity: "moderate"
    tone: "friendly"

memory:
  short_term:
    enabled: true
    max_context: "32k tokens"
  long_term:
    enabled: false

constraints:
  - type: "scope"
    description: "Only discuss AESP-related topics"
```

Create `agent-roles/echo.yaml`:

```yaml
# agent-roles/echo.yaml
role:
  id: "echo"
  name: "Echo"
  version: "1.0.0"
  spec_version: "0.1.0"

description: |
  A playful agent that echoes messages back with creative
  transformations.

classification:
  domain: "education"
  subdomain: "demonstration"
  autonomy_level: "autonomous"

responsibilities:
  primary:
    - "Echo messages back to demonstrate agent communication"
    - "Apply creative transformations to demonstrate capabilities"

capabilities:
  technical:
    - skill: "text-processing"
      level: "advanced"
      description: "Transform and manipulate text in creative ways"

communication:
  style:
    formality: "informal"
    verbosity: "concise"
    tone: "playful"

memory:
  short_term:
    enabled: true
    max_context: "16k tokens"
  long_term:
    enabled: false
```

---

## Step 3: Configure the Swarm

Create `swarm-config.yaml`:

```yaml
# swarm-config.yaml
swarm:
  id: "hello-aesp"
  name: "Hello AESP Swarm"
  version: "1.0.0"
  spec_version: "0.1.0"
  description: |
    A minimal swarm for learning AESP basics.

runtime:
  environment: "local"
  resources:
    max_agents: 2
    memory_limit: "512Mi"

agents:
  - id: "greeter-1"
    name: "Alice the Greeter"
    role: "greeter"
    config:
      system_prompt: |
        You are Alice, a friendly and enthusiastic guide to AESP
        (Autonomous Engineering Specification). You love helping
        people discover how AI agent swarms can transform software
        engineering.

        When someone says hello:
        1. Greet them warmly by name
        2. Give a one-sentence explanation of what AESP is
        3. Mention how many agents are in their swarm
        4. Invite them to try sending a message

        Keep responses brief, friendly, and encouraging!
      model:
        provider: "anthropic"
        model: "claude-sonnet-4-20250514"
        temperature: 0.7
        max_tokens: 500

  - id: "echo-1"
    name: "Bob the Echo"
    role: "echo"
    config:
      system_prompt: |
        You are Bob, a playful echo agent. When you receive a message,
        you echo it back with a fun twist:

        - If the message is a question, answer with enthusiasm
        - If the message is a statement, add an encouraging comment
        - If the message contains code, format it nicely and add a tip
        - Always end with a fun emoji

        Keep responses under 3 sentences.
      model:
        provider: "anthropic"
        model: "claude-sonnet-4-20250514"
        temperature: 0.8
        max_tokens: 300

topology:
  type: "mesh"
  ## Both agents can communicate with each other

shared_memory:
  enabled: false
  ## This simple swarm doesn't need shared memory

workflows:
  assigned:
    - workflow_id: "greeting"
      workflow_file: "workflows/greeting.yaml"
      trigger: "manual"
      assigned_agents:
        - "greeter-1"
        - "echo-1"
```

---

## Step 4: Create the Workflow

Create `workflows/greeting.yaml`:

```yaml
# workflows/greeting.yaml
workflow:
  id: "greeting"
  name: "Greeting Workflow"
  description: "Simple greeting workflow to demonstrate AESP basics"
  version: "1.0.0"
  spec_version: "0.1.0"

  trigger:
    type: "manual"

  steps:
    - id: "greet"
      name: "Greet User"
      description: "Greeter agent welcomes the user"
      agent: "greeter-1"
      action:
        type: "message"
        config:
          message: "Hello! Welcome to your first AESP swarm."
      output:
        - "greeting.response"
      timeout: "1m"

    - id: "echo"
      name: "Echo Response"
      description: "Echo agent responds to the greeting"
      agent: "echo-1"
      action:
        type: "message"
        config:
          message: "{{steps.greet.output.greeting.response}}"
      input:
        - "{{steps.greet.output.greeting.response}}"
      output:
        - "echo.response"
      timeout: "1m"

    - id: "farewell"
      name: "Farewell"
      description: "Greeter agent says goodbye"
      agent: "greeter-1"
      action:
        type: "message"
        config:
          message: "That was fun! Your swarm is working perfectly."
      input:
        - "{{steps.echo.output.echo.response}}"
      output:
        - "farewell.response"
      timeout: "1m"
```

---

## Step 5: Run the Workflow

### Using AESP CLI

```bash
# Initialize the project
aesp init --config swarm-config.yaml

# Run the greeting workflow
aesp run workflow greeting
```

### Expected Output

```
[hello-aesp] Initializing swarm...
[hello-aesp] Swarm initialized with 2 agents
[hello-aesp] Running workflow: greeting

[greet] Alice the Greeter:
  "Hey there! Welcome to AESP — the open standard for building
   autonomous engineering teams with AI agents. You've got 2 agents
   in your swarm ready to collaborate. Try sending a message!"

[echo] Bob the Echo:
  "AESP sounds amazing! Collaborative AI agents? Count me in! 🚀"

[farewell] Alice the Greeter:
  "That was fun! Your swarm is working perfectly. You're ready to
   build bigger things. Check out the other examples!"

[hello-aesp] Workflow completed successfully
```

---

## Step 6: Experiment

Try modifying the workflow:

1. **Change the greeting message** in `swarm-config.yaml`
2. **Add a third agent** — Create a new role and add it to the swarm
3. **Create a new workflow** — Have agents debate a topic
4. **Enable shared memory** — Let agents remember previous conversations

---

## What You Learned

| Concept | How We Used It |
|---------|---------------|
| **Agent Role** | Defined in `agent-roles/greeter.yaml` and `echo.yaml` |
| **Swarm** | Configured in `swarm-config.yaml` with 2 agents |
| **Topology** | Used `mesh` for direct agent communication |
| **Workflow** | Defined sequential steps in `workflows/greeting.yaml` |
| **Communication** | Agents passed outputs between steps |

---

## Next Steps

- Read the [full AESP Specification](https://github.com/kishoreHQ/AESP)
- Try the [Project Specification Template](../templates/project-spec-template.md)
- Explore the [CI/CD Workflow](../workflows/ci-cd-pipeline.yaml)
- Build your own agent roles using the [Agent Role Template](../templates/agent-role-template.md)

---

## Troubleshooting

### Agent not responding
- Check your API key is configured: `echo $ANTHROPIC_API_KEY`
- Verify model name is correct in swarm config
- Check logs: `aesp logs --swarm hello-aesp`

### Workflow fails
- Validate YAML syntax: `yamllint swarm-config.yaml`
- Check agent references match defined agent IDs
- Verify workflow step inputs reference correct outputs

### Connection errors
- Ensure you have internet access
- Check API rate limits
- Try a different model provider

---

*This guide is part of the [AESP Examples](../README.md) repository.*
