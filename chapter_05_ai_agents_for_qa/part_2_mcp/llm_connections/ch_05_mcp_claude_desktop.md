# MCP Claude Desktop Setup

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Connect MCP servers to Claude Desktop for AI-powered QA workflows.

---

## 📦 Prerequisites

- Claude Desktop installed (macOS or Windows)
- Node.js 18+ installed
- MCP server you want to connect

---

## 🛠️ Configuration

### Step 1: Find Config File

**macOS:**
```bash
~/Library/Application Support/Claude/claude_desktop_config.json
```

**Windows:**
```
%APPDATA%\Claude\claude_desktop_config.json
```

### Step 2: Add MCP Server

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-playwright"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/project"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token"
      }
    }
  }
}
```

### Step 3: Restart Claude Desktop

Close and reopen Claude Desktop to load the new configuration.

---

## ✅ Verify Connection

1. Open Claude Desktop
2. Click the 🔌 plug icon in the input area
3. You should see your MCP servers listed
4. Ask Claude: "What MCP tools do you have access to?"

---

## 📝 Example: Playwright MCP

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-playwright"]
    }
  }
}
```

Now you can say:
- "Take a screenshot of google.com"
- "Navigate to my app and click the login button"
- "Fill the login form with test credentials"

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| Server not appearing | Check JSON syntax, restart Claude |
| Command not found | Ensure Node.js is in PATH |
| Permission denied | Check file permissions |
| Tool errors | Check server logs in terminal |

---

## 📚 See Also

- [MCP Cursor Setup](ch_05_mcp_cursor.md)
- [MCP VS Code Setup](ch_05_mcp_vscode.md)
