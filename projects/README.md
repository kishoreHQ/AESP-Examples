# AESP Sample Projects

> **Complete sample projects demonstrating AESP in action.**

This directory contains end-to-end example projects that show how to apply the Autonomous Engineering Specification to real-world scenarios. Each project includes agent configurations, swarm definitions, workflows, and documentation.

---

## Available Projects

### Hello AESP
**File:** [`hello-aesp.md`](hello-aesp.md)

A step-by-step "Hello World" guide for getting started with AESP. This project walks you through:
- Setting up your first agent
- Creating a minimal swarm
- Running a simple workflow
- Understanding the basics

**Complexity**: Beginner | **Time**: 15 minutes

---

## Project Structure

Each sample project follows this structure:

```
projects/
├── README.md              # This file
└── hello-aesp.md          # Getting started guide
```

Future projects will include:

```
projects/
├── web-app/               # Full-stack web application
│   ├── swarm-config.yaml
│   ├── agent-roles/
│   ├── workflows/
│   └── README.md
├── api-service/           # REST API microservice
│   ├── swarm-config.yaml
│   ├── agent-roles/
│   ├── workflows/
│   └── README.md
└── data-pipeline/         # ETL data pipeline
    ├── swarm-config.yaml
    ├── agent-roles/
    ├── workflows/
    └── README.md
```

---

## Using Sample Projects

1. Choose a project matching your use case
2. Read the project README for prerequisites
3. Copy the configuration files to your project
4. Customize agent roles and workflows
5. Run with your AESP runtime

---

## Contributing Projects

See [CONTRIBUTING.md](../CONTRIBUTING.md). Sample projects should:

- Include a complete, working configuration
- Document all prerequisites
- Provide step-by-step setup instructions
- Include realistic agent roles and workflows
- Be tested with the latest AESP runtime

---

*Part of the [AESP Examples](../README.md) repository.*
