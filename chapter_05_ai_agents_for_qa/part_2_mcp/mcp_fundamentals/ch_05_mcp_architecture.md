# MCP Architecture

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    MCP ARCHITECTURE                              │
└─────────────────────────────────────────────────────────────────┘

    MCP CLIENTS                    MCP SERVERS
    ───────────                    ───────────
┌──────────────┐               ┌──────────────────┐
│ Claude       │               │ Playwright MCP   │
│ Desktop      │ ←──────────→  │   - run_tests    │
└──────────────┘    MCP        │   - take_screen  │
                  Protocol     └──────────────────┘
┌──────────────┐               
│ Cursor       │               ┌──────────────────┐
│              │ ←──────────→  │ Jira MCP         │
└──────────────┘               │   - create_bug   │
                               │   - search_issues│
┌──────────────┐               └──────────────────┘
│ VS Code +    │               
│ Continue     │ ←──────────→  ┌──────────────────┐
└──────────────┘               │ GitHub MCP       │
                               │   - create_pr    │
                               │   - read_file    │
                               └──────────────────┘
```

---

## 🧩 Core Components

### 1. MCP Client
The AI application that uses tools.

| Client | Type | Description |
|--------|------|-------------|
| Claude Desktop | Native | Built-in MCP support |
| Cursor | IDE | Code editor with AI |
| Continue | Extension | VS Code AI assistant |
| Custom App | Custom | Your own application |

### 2. MCP Server
Exposes tools and resources.

```javascript
// Example MCP Server structure
const server = new MCPServer({
  name: "qa-tools",
  version: "1.0.0"
});

// Register a tool
server.tool("run_tests", {
  description: "Run Playwright tests",
  parameters: {
    testFile: { type: "string", required: true }
  },
  handler: async ({ testFile }) => {
    return await runPlaywright(testFile);
  }
});
```

### 3. Tools
Functions the AI can call.

```json
{
  "name": "create_bug",
  "description": "Create a bug ticket in Jira",
  "inputSchema": {
    "type": "object",
    "properties": {
      "title": { "type": "string" },
      "description": { "type": "string" },
      "priority": { "type": "string", "enum": ["P0", "P1", "P2", "P3"] }
    },
    "required": ["title", "description"]
  }
}
```

### 4. Resources
Data sources the AI can read.

```json
{
  "uri": "file:///project/tests/",
  "name": "Test Files",
  "description": "All test files in the project"
}
```

### 5. Prompts
Pre-built instruction templates.

```json
{
  "name": "analyze_test_failure",
  "description": "Analyze why a test failed",
  "arguments": [
    { "name": "test_name", "required": true },
    { "name": "error_log", "required": true }
  ]
}
```

---

## 🔄 Communication Flow

```
┌──────────────────────────────────────────────────────────────────┐
│                    REQUEST/RESPONSE FLOW                         │
└──────────────────────────────────────────────────────────────────┘

User: "Run login tests"
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│                      CLAUDE (MCP Client)                         │
│  1. Receives user request                                        │
│  2. Checks available tools from connected MCP servers            │
│  3. Decides to call "run_tests" tool                            │
│  4. Formats request: { tool: "run_tests", args: {...} }         │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼ JSON-RPC over stdio/SSE
┌─────────────────────────────────────────────────────────────────┐
│                    PLAYWRIGHT MCP SERVER                         │
│  1. Receives tool call request                                   │
│  2. Validates parameters                                         │
│  3. Executes: npx playwright test login.spec.ts                 │
│  4. Returns result: { passed: 5, failed: 1, output: "..." }     │
└─────────────────────────────────────────────────────────────────┘
          │
          ▼
┌─────────────────────────────────────────────────────────────────┐
│                      CLAUDE (MCP Client)                         │
│  1. Receives result                                              │
│  2. Formats response for user                                    │
│  3. "I ran your login tests: 5 passed, 1 failed..."             │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📋 Transport Options

| Transport | Use Case | Description |
|-----------|----------|-------------|
| **stdio** | Local | Standard input/output |
| **SSE** | Remote | Server-Sent Events over HTTP |
| **WebSocket** | Real-time | Bidirectional streaming |

---

## 📚 See Also

- [What is MCP?](ch_05_what_is_mcp.md)
- [Build MCP Server (JS)](../build_mcp_server/ch_05_mcp_server_js.md)
