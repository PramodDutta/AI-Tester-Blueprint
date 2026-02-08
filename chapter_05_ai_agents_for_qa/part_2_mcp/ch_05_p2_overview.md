# Part 2: MCP (Model Context Protocol) Overview

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Master MCP for building AI-powered QA tools  
**Chapter:** 5 - AI Agents for QA  
**Part:** 2 - MCP (Model Context Protocol)  
**Estimated Time:** 6-8 hours

---

## 🎯 What You'll Learn

By the end of Part 2, you will be able to:

1. ✅ Understand what MCP is and how it works
2. ✅ Build local QA tools using MCP
3. ✅ Connect MCP tools to Claude Desktop, Cursor, VS Code
4. ✅ Create your own MCP server in JS/TypeScript or Python
5. ✅ Build a practical automation healing agent

---

## 📋 Part 2 Contents

| Section | Topics | Time |
|---------|--------|------|
| [What is MCP?](mcp_fundamentals/ch_05_what_is_mcp.md) | Protocol overview, architecture | 1h |
| [MCP Architecture](mcp_fundamentals/ch_05_mcp_architecture.md) | Servers, clients, tools | 1h |
| [Building QA Tools](building_qa_tools/ch_05_mcp_code_review_tool.md) | Code Review, API Testing, Playwright | 2h |
| [LLM Connections](llm_connections/ch_05_mcp_claude_desktop.md) | Claude, Cursor, VS Code setup | 1h |
| [Build MCP Server](build_mcp_server/ch_05_mcp_server_js.md) | JS/TS and Python implementation | 2h |
| [Mini-Project](mini_project/ch_05_automation_healing_agent.md) | Self-healing test agent | 1h |

---

## ❓ Why MCP?

```
┌─────────────────────────────────────────────────────────────────┐
│                      THE PROBLEM                                │
└─────────────────────────────────────────────────────────────────┘

Before MCP:
  LLM ←──── Custom Integration 1 ───→ Jira
  LLM ←──── Custom Integration 2 ───→ GitHub  
  LLM ←──── Custom Integration 3 ───→ Playwright
  LLM ←──── Custom Integration 4 ───→ Database
  
  ❌ Each tool needs custom code
  ❌ Different for each LLM
  ❌ Hard to maintain

┌─────────────────────────────────────────────────────────────────┐
│                      THE SOLUTION: MCP                          │
└─────────────────────────────────────────────────────────────────┘

With MCP:
                    ┌─────────────────┐
  Claude     ───────┤                 ├───→ Jira
  Cursor     ───────┤   MCP Server    ├───→ GitHub
  VS Code    ───────┤   (Standard)    ├───→ Playwright
  Any LLM    ───────┤                 ├───→ Database
                    └─────────────────┘
  
  ✅ One standard protocol
  ✅ Works with any MCP client
  ✅ Easy to share and reuse
```

---

## 🧩 Key Concepts

| Concept | Description |
|---------|-------------|
| **MCP Server** | Exposes tools/resources via the protocol |
| **MCP Client** | Consumes tools (Claude, Cursor, etc.) |
| **Tool** | A function the LLM can call |
| **Resource** | Data the LLM can read |
| **Prompt** | Pre-built instructions |

---

## 🛠️ Tools We'll Build

| Tool | Purpose | Section |
|------|---------|---------|
| Code Review Tool | AI-powered code analysis | Building QA Tools |
| API Test Tool | Test APIs automatically | Building QA Tools |
| Playwright Tool | E2E test generation | Building QA Tools |
| Healing Agent | Self-fix broken tests | Mini-Project |

---

## 📁 Part 2 File Structure

```
part_2_mcp/
├── ch_05_p2_overview.md           # This file
├── mcp_fundamentals/
│   ├── ch_05_what_is_mcp.md
│   └── ch_05_mcp_architecture.md
├── building_qa_tools/
│   ├── ch_05_mcp_code_review_tool.md
│   ├── ch_05_mcp_api_testing_tool.md
│   └── ch_05_mcp_playwright_tool.md
├── llm_connections/
│   ├── ch_05_mcp_claude_desktop.md
│   ├── ch_05_mcp_cursor.md
│   └── ch_05_mcp_vscode.md
├── build_mcp_server/
│   ├── ch_05_mcp_server_js.md
│   └── ch_05_mcp_server_python.md
└── mini_project/
    └── ch_05_automation_healing_agent.md
```

---

## 🚀 Prerequisites

Before starting Part 2, ensure you have:

- ✅ Completed Part 1 (Agent Fundamentals)
- ✅ Node.js 18+ installed
- ✅ Python 3.10+ installed
- ✅ Claude Desktop or Cursor installed
- ✅ Basic understanding of APIs

---

## 📚 Navigation

| Previous | Up | Next |
|----------|------|------|
| [Part 1: Fundamentals](../part_1_fundamentals/ch_05_p1_overview.md) | [Chapter 5](../ch_05_ai_agents_for_qa.md) | [Part 3: No-Code Platforms](../part_3_no_code/ch_05_p3_overview.md) |
