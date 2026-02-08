# MCP Cursor Setup

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Cursor IDE has built-in MCP support for powerful AI coding with external tools.

---

## 🛠️ Configuration

### Step 1: Open Cursor Settings

1. Open Cursor
2. Go to Settings (⌘ + ,)
3. Search for "MCP"

### Step 2: Add MCP Servers

Create or edit `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-playwright"]
    },
    "filesystem": {
      "command": "npx", 
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "."]
    }
  }
}
```

### Step 3: Restart Cursor

Reload the window or restart Cursor.

---

## ✅ Verify Connection

1. Open Cursor chat (⌘ + L)
2. Type: "What MCP tools are available?"
3. You should see the connected tools listed

---

## 💡 Usage Examples

```
You: "Run the login tests using Playwright"
Cursor: [Uses playwright MCP to execute tests]

You: "Create a new test file for the checkout flow"
Cursor: [Uses filesystem MCP to create file]

You: "Take a screenshot of the app after login"
Cursor: [Uses playwright MCP for screenshot]
```

---

## 📚 See Also

- [MCP Claude Desktop](ch_05_mcp_claude_desktop.md)
- [MCP VS Code Setup](ch_05_mcp_vscode.md)
