# What is MCP?

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 The Model Context Protocol

**MCP (Model Context Protocol)** is an open standard by Anthropic for connecting AI models to external tools and data sources.

> **Think of MCP as:** USB for AI — a universal standard that lets any AI connect to any tool.

---

## 🔌 The USB Analogy

```
USB (Universal Serial Bus)          MCP (Model Context Protocol)
─────────────────────────           ──────────────────────────────
Any device + Any computer           Any tool + Any AI model
    ↓                                   ↓
Standard connector                  Standard protocol
    ↓                                   ↓
Plug and play                       Connect and use
```

---

## 📋 Key Features

| Feature | Description |
|---------|-------------|
| **Open Standard** | Anyone can implement |
| **Tool Calling** | AI can invoke functions |
| **Resource Access** | AI can read data |
| **Prompt Templates** | Reusable instructions |
| **Bidirectional** | Client ↔ Server communication |

---

## 🏗️ How MCP Works

```
┌─────────────────────────────────────────────────────────────────┐
│                        MCP WORKFLOW                              │
└─────────────────────────────────────────────────────────────────┘

1. User asks Claude: "Run my Playwright tests"

2. Claude checks available MCP tools:
   └── playwright_mcp has "run_tests" tool

3. Claude calls the tool:
   └── { "tool": "run_tests", "args": { "file": "login.spec.ts" } }

4. MCP Server executes:
   └── npx playwright test login.spec.ts

5. MCP Server returns result:
   └── "5 tests passed, 1 failed"

6. Claude responds to user:
   └── "Your tests ran: 5 passed, 1 failed. The failing test..."
```

---

## 🎯 MCP for QA

| Use Case | How MCP Helps |
|----------|---------------|
| Run tests | Claude can execute Playwright directly |
| File bugs | Claude can create Jira tickets |
| Analyze code | Claude can read your codebase |
| Generate tests | Claude can write to test files |
| Check results | Claude can query test databases |

---

## 🆚 Before vs After MCP

### Before MCP
```python
# Custom integration for each tool + each AI
claude_jira_plugin = build_custom_integration("claude", "jira")
cursor_jira_plugin = build_custom_integration("cursor", "jira")
vscode_jira_plugin = build_custom_integration("vscode", "jira")
# Repeat for every combination...
```

### After MCP
```python
# One MCP server works with all AI clients
jira_mcp_server = JiraMCPServer()  # Works with Claude, Cursor, VS Code, etc.
```

---

## 🔗 Official Resources

- [MCP Documentation](https://modelcontextprotocol.io)
- [MCP GitHub](https://github.com/modelcontextprotocol)
- [MCP Servers Directory](https://github.com/modelcontextprotocol/servers)

---

## 📚 See Also

- [MCP Architecture](ch_05_mcp_architecture.md)
- [Building QA Tools](../building_qa_tools/ch_05_mcp_code_review_tool.md)
