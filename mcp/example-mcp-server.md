# Building an MCP Server for AESP

> **Complete guide to creating an MCP server that integrates with AESP agent swarms.**
>
> **AESP Reference:** AESP-0008 (Tool Integration), AESP-0009 (Security)

---

## Overview

This guide walks you through building a production-ready MCP server that enables AESP agents to interact with external systems. We'll build a **Project Management MCP Server** as an example — allowing agents to read project status, create tasks, and update milestones.

---

## Prerequisites

- Node.js 18+ or Python 3.10+
- Understanding of MCP protocol (see [modelcontextprotocol.io](https://modelcontextprotocol.io))
- AESP runtime environment (or compatible agent framework)

---

## Server Architecture

```
+-----------------+        MCP Protocol        +------------------+
|   AESP Agent    |  <--------------------->   |   MCP Server     |
|   (Client)      |    stdio / SSE / HTTP      |   (Your Code)    |
+-----------------+                            +------------------+
                                                         |
                                               +---------+---------+
                                               |                   |
                                       +-------+------+   +-------+------+
                                       |  Project API |   |  Database    |
                                       |  (External)  |   |  (Local)     |
                                       +--------------+   +--------------+
```

---

## Implementation (Node.js/TypeScript)

### Step 1: Project Setup

```bash
mkdir aesp-mcp-project-server
cd aesp-mcp-project-server
npm init -y
npm install @modelcontextprotocol/sdk zod
npm install -D typescript @types/node
npx tsc --init
```

### Step 2: Server Implementation

```typescript
// src/server.ts
import { Server } from '@modelcontextprotocol/sdk/server/index.js';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio.js';
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
  ListResourcesRequestSchema,
  ReadResourceRequestSchema,
} from '@modelcontextprotocol/sdk/types.js';
import { z } from 'zod';

// Tool input schemas
const CreateTaskSchema = z.object({
  title: z.string().min(1).max(200),
  description: z.string().optional(),
  assignee: z.string().optional(),
  priority: z.enum(['low', 'medium', 'high', 'urgent']).default('medium'),
  due_date: z.string().datetime().optional(),
  labels: z.array(z.string()).optional(),
});

const UpdateTaskSchema = z.object({
  task_id: z.string(),
  status: z.enum(['todo', 'in_progress', 'review', 'done']).optional(),
  title: z.string().optional(),
  description: z.string().optional(),
  assignee: z.string().optional(),
});

const GetProjectMetricsSchema = z.object({
  project_id: z.string(),
  time_range: z.enum(['7d', '30d', '90d']).default('30d'),
});

// Server implementation
class ProjectManagementMCPServer {
  private server: Server;
  private apiClient: ProjectAPIClient;

  constructor() {
    this.apiClient = new ProjectAPIClient({
      baseUrl: process.env.PROJECT_API_URL!,
      apiKey: process.env.PROJECT_API_KEY!,
    });

    this.server = new Server(
      {
        name: 'aesp-project-management',
        version: '1.0.0',
      },
      {
        capabilities: {
          tools: {},
          resources: {},
        },
      }
    );

    this.setupHandlers();
  }

  private setupHandlers() {
    // List available tools
    this.server.setRequestHandler(ListToolsRequestSchema, async () => {
      return {
        tools: [
          {
            name: 'create_task',
            description: 'Create a new task in the project management system',
            inputSchema: {
              type: 'object',
              properties: {
                title: { type: 'string', description: 'Task title' },
                description: { type: 'string', description: 'Task description' },
                assignee: { type: 'string', description: 'User to assign the task to' },
                priority: {
                  type: 'string',
                  enum: ['low', 'medium', 'high', 'urgent'],
                  default: 'medium',
                },
                due_date: { type: 'string', format: 'date-time' },
                labels: { type: 'array', items: { type: 'string' } },
              },
              required: ['title'],
            },
          },
          {
            name: 'update_task',
            description: 'Update an existing task',
            inputSchema: {
              type: 'object',
              properties: {
                task_id: { type: 'string' },
                status: { type: 'string', enum: ['todo', 'in_progress', 'review', 'done'] },
                title: { type: 'string' },
                description: { type: 'string' },
                assignee: { type: 'string' },
              },
              required: ['task_id'],
            },
          },
          {
            name: 'get_project_metrics',
            description: 'Get project health metrics and KPIs',
            inputSchema: {
              type: 'object',
              properties: {
                project_id: { type: 'string' },
                time_range: { type: 'string', enum: ['7d', '30d', '90d'] },
              },
              required: ['project_id'],
            },
          },
          {
            name: 'list_tasks',
            description: 'List tasks with optional filtering',
            inputSchema: {
              type: 'object',
              properties: {
                project_id: { type: 'string' },
                status: { type: 'string', enum: ['todo', 'in_progress', 'review', 'done'] },
                assignee: { type: 'string' },
                limit: { type: 'number', default: 50 },
              },
              required: ['project_id'],
            },
          },
        ],
      };
    });

    // Execute tool calls
    this.server.setRequestHandler(CallToolRequestSchema, async (request) => {
      const { name, arguments: args } = request.params;

      // Input validation and execution
      switch (name) {
        case 'create_task': {
          const input = CreateTaskSchema.parse(args);
          const task = await this.apiClient.createTask(input);
          return {
            content: [
              {
                type: 'text',
                text: `Task created successfully:\nID: ${task.id}\nTitle: ${task.title}\nPriority: ${task.priority}\nURL: ${task.url}`,
              },
            ],
          };
        }

        case 'update_task': {
          const input = UpdateTaskSchema.parse(args);
          const task = await this.apiClient.updateTask(input.task_id, input);
          return {
            content: [
              {
                type: 'text',
                text: `Task ${task.id} updated successfully.\nStatus: ${task.status}\nTitle: ${task.title}`,
              },
            ],
          };
        }

        case 'get_project_metrics': {
          const input = GetProjectMetricsSchema.parse(args);
          const metrics = await this.apiClient.getMetrics(
            input.project_id,
            input.time_range
          );
          return {
            content: [
              {
                type: 'text',
                text: JSON.stringify(metrics, null, 2),
              },
            ],
          };
        }

        case 'list_tasks': {
          const { project_id, status, assignee, limit = 50 } = args as any;
          const tasks = await this.apiClient.listTasks({
            project_id,
            status,
            assignee,
            limit,
          });
          const summary = tasks.map(
            (t: any) => `- [${t.status}] ${t.title} (${t.priority}) - ${t.assignee || 'unassigned'}`
          );
          return {
            content: [
              {
                type: 'text',
                text: `Found ${tasks.length} tasks:\n${summary.join('\n')}`,
              },
            ],
          };
        }

        default:
          throw new Error(`Unknown tool: ${name}`);
      }
    });

    // List available resources
    this.server.setRequestHandler(ListResourcesRequestSchema, async () => {
      return {
        resources: [
          {
            uri: 'project://active',
            name: 'Active Projects',
            mimeType: 'application/json',
            description: 'List of currently active projects',
          },
          {
            uri: 'project://metrics/summary',
            name: 'Project Metrics Summary',
            mimeType: 'application/json',
            description: 'High-level metrics across all projects',
          },
        ],
      };
    });

    // Read resource content
    this.server.setRequestHandler(ReadResourceRequestSchema, async (request) => {
      const { uri } = request.params;

      switch (uri) {
        case 'project://active': {
          const projects = await this.apiClient.listProjects({ status: 'active' });
          return {
            contents: [
              {
                uri,
                mimeType: 'application/json',
                text: JSON.stringify(projects, null, 2),
              },
            ],
          };
        }

        case 'project://metrics/summary': {
          const metrics = await this.apiClient.getMetricsSummary();
          return {
            contents: [
              {
                uri,
                mimeType: 'application/json',
                text: JSON.stringify(metrics, null, 2),
              },
            ],
          };
        }

        default:
          throw new Error(`Unknown resource: ${uri}`);
      }
    });
  }

  async start() {
    const transport = new StdioServerTransport();
    await this.server.connect(transport);
    console.error('Project Management MCP Server running on stdio');
  }
}

// API Client
class ProjectAPIClient {
  constructor(private config: { baseUrl: string; apiKey: string }) {}

  async createTask(data: any) {
    const response = await fetch(`${this.config.baseUrl}/tasks`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${this.config.apiKey}`,
      },
      body: JSON.stringify(data),
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }

  async updateTask(id: string, data: any) {
    const response = await fetch(`${this.config.baseUrl}/tasks/${id}`, {
      method: 'PATCH',
      headers: {
        'Content-Type': 'application/json',
        Authorization: `Bearer ${this.config.apiKey}`,
      },
      body: JSON.stringify(data),
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }

  async getMetrics(projectId: string, timeRange: string) {
    const response = await fetch(
      `${this.config.baseUrl}/projects/${projectId}/metrics?range=${timeRange}`,
      {
        headers: { Authorization: `Bearer ${this.config.apiKey}` },
      }
    );
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }

  async listTasks(filters: any) {
    const params = new URLSearchParams(filters);
    const response = await fetch(`${this.config.baseUrl}/tasks?${params}`, {
      headers: { Authorization: `Bearer ${this.config.apiKey}` },
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }

  async listProjects(filters: any) {
    const params = new URLSearchParams(filters);
    const response = await fetch(`${this.config.baseUrl}/projects?${params}`, {
      headers: { Authorization: `Bearer ${this.config.apiKey}` },
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }

  async getMetricsSummary() {
    const response = await fetch(`${this.config.baseUrl}/metrics/summary`, {
      headers: { Authorization: `Bearer ${this.config.apiKey}` },
    });
    if (!response.ok) throw new Error(`API error: ${response.status}`);
    return response.json();
  }
}

// Start server
const server = new ProjectManagementMCPServer();
server.start().catch(console.error);
```

### Step 3: Package Configuration

```json
// package.json
{
  "name": "@aesp/mcp-project-management",
  "version": "1.0.0",
  "description": "MCP server for project management integration with AESP",
  "type": "module",
  "main": "dist/server.js",
  "scripts": {
    "build": "tsc",
    "start": "node dist/server.js",
    "dev": "tsc --watch"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.0.0",
    "zod": "^3.22.0"
  },
  "devDependencies": {
    "@types/node": "^20.0.0",
    "typescript": "^5.3.0"
  }
}
```

### Step 4: Environment Configuration

```bash
# .env
PROJECT_API_URL=https://api.projectmgmt.example.com/v1
PROJECT_API_KEY=your_api_key_here
```

---

## AESP Integration

### Agent Configuration

Add the MCP server to your AESP agent configuration:

```yaml
# swarm-config.yaml
agents:
  - id: "project-manager-1"
    name: "Project Manager"
    role: "project-coordinator"
    config:
      system_prompt: "file://prompts/project-coordinator.md"
      model:
        provider: "anthropic"
        model: "claude-sonnet-4-20250514"
    mcp_servers:
      - name: "project-management"
        command: "node"
        args: ["/path/to/aesp-mcp-project-server/dist/server.js"]
        env:
          PROJECT_API_URL: "{{secrets.project_api_url}}"
          PROJECT_API_KEY: "{{secrets.project_api_key}}"
```

### Usage Example

With this MCP server configured, an agent can:

```
User: "Create a high-priority task to fix the authentication bug
      and assign it to the security team"

Agent: [Calls create_task tool via MCP]
       Task created:
       ID: TASK-4821
       Title: Fix authentication bug
       Priority: high
       Assignee: security-team
       URL: https://projects.example.com/TASK-4821
```

---

## Best Practices

### 1. Input Validation
Always validate inputs using Zod or similar schema validation:

```typescript
const schema = z.object({
  title: z.string().min(1).max(200),
  priority: z.enum(['low', 'medium', 'high']),
});
// Validates and provides type safety
```

### 2. Error Handling
Return meaningful error messages to the agent:

```typescript
try {
  const result = await apiClient.createTask(data);
  return { content: [{ type: 'text', text: `Created: ${result.id}` }] };
} catch (error) {
  return {
    content: [{ type: 'text', text: `Error: ${error.message}. Please check your API credentials.` }],
    isError: true,
  };
}
```

### 3. Audit Logging
Log all tool invocations for security and compliance:

```typescript
console.error(JSON.stringify({
  timestamp: new Date().toISOString(),
  tool: name,
  args: sanitize(args),
  agent_id: request.context?.agent_id,
}));
```

### 4. Rate Limiting
Protect external APIs from excessive calls:

```typescript
import { RateLimiter } from 'limiter';
const limiter = new RateLimiter({ tokensPerInterval: 100, interval: 'minute' });
```

### 5. Secrets Management
Never hardcode credentials. Use environment variables or secret stores:

```yaml
# Good
env:
  API_KEY: "{{secrets.api_key}}"

# Bad
env:
  API_KEY: "sk-1234567890"
```

---

## Testing Your MCP Server

```typescript
// tests/server.test.ts
import { describe, it, expect } from 'vitest';
import { Client } from '@modelcontextprotocol/sdk/client/index.js';

describe('Project Management MCP Server', () => {
  it('should list available tools', async () => {
    const client = new Client({ name: 'test', version: '1.0.0' });
    // ... setup transport
    const tools = await client.listTools();
    expect(tools.tools.map(t => t.name)).toContain('create_task');
  });

  it('should create a task', async () => {
    const result = await client.callTool({
      name: 'create_task',
      arguments: {
        title: 'Test Task',
        priority: 'medium',
      },
    });
    expect(result.content[0].text).toContain('created successfully');
  });
});
```

---

## Deployment

### Docker

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY dist/ ./dist/
EXPOSE 3000
CMD ["node", "dist/server.js"]
```

### Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `PROJECT_API_URL` | Yes | Base URL of the project management API |
| `PROJECT_API_KEY` | Yes | API authentication key |
| `LOG_LEVEL` | No | Logging level (debug, info, warn, error) |
| `RATE_LIMIT_RPM` | No | Rate limit in requests per minute (default: 100) |
| `REQUEST_TIMEOUT` | No | Request timeout in ms (default: 30000) |

---

## Resources

- [MCP Protocol Documentation](https://modelcontextprotocol.io)
- [MCP SDK for TypeScript](https://github.com/modelcontextprotocol/typescript-sdk)
- [AESP Tool Integration Spec](https://github.com/kishoreHQ/AESP/blob/main/docs/AESP-0008.md)

---

*Generated from AESP MCP Integration Guide v1.0.0*
