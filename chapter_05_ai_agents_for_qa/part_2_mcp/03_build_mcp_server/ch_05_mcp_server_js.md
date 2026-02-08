# Build MCP Server (JavaScript/TypeScript)

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Build your own MCP server to expose custom QA tools to AI assistants.

---

## 📦 Setup

```bash
mkdir qa-mcp-server
cd qa-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk
```

---

## 📝 Basic Server

```typescript
// src/index.ts
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  {
    name: "qa-tools",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {},
    },
  }
);

// Define a tool
server.setRequestHandler("tools/list", async () => ({
  tools: [
    {
      name: "run_tests",
      description: "Run Playwright tests",
      inputSchema: {
        type: "object",
        properties: {
          testFile: {
            type: "string",
            description: "Test file to run",
          },
        },
        required: ["testFile"],
      },
    },
    {
      name: "analyze_failure",
      description: "Analyze a test failure",
      inputSchema: {
        type: "object",
        properties: {
          errorLog: {
            type: "string",
            description: "Error log from failed test",
          },
        },
        required: ["errorLog"],
      },
    },
  ],
}));

// Handle tool calls
server.setRequestHandler("tools/call", async (request) => {
  const { name, arguments: args } = request.params;

  if (name === "run_tests") {
    const { testFile } = args;
    // Execute tests
    const result = await runPlaywrightTest(testFile);
    return {
      content: [
        {
          type: "text",
          text: JSON.stringify(result, null, 2),
        },
      ],
    };
  }

  if (name === "analyze_failure") {
    const { errorLog } = args;
    // Analyze the error
    const analysis = analyzeError(errorLog);
    return {
      content: [
        {
          type: "text",
          text: analysis,
        },
      ],
    };
  }

  throw new Error(`Unknown tool: ${name}`);
});

// Helper functions
async function runPlaywrightTest(testFile: string) {
  const { execSync } = require("child_process");
  try {
    const output = execSync(`npx playwright test ${testFile}`, {
      encoding: "utf-8",
    });
    return { success: true, output };
  } catch (error) {
    return { success: false, error: error.message };
  }
}

function analyzeError(errorLog: string) {
  // Simple analysis logic
  if (errorLog.includes("timeout")) {
    return "This appears to be a timeout issue. Consider increasing wait times.";
  }
  if (errorLog.includes("element not found")) {
    return "Element not found. The selector may have changed.";
  }
  return "Unable to determine specific cause. Please review the full log.";
}

// Start server
const transport = new StdioServerTransport();
server.connect(transport);
```

---

## 🔧 Package.json

```json
{
  "name": "qa-mcp-server",
  "version": "1.0.0",
  "type": "module",
  "bin": {
    "qa-mcp": "./dist/index.js"
  },
  "scripts": {
    "build": "tsc",
    "start": "node dist/index.js"
  },
  "dependencies": {
    "@modelcontextprotocol/sdk": "^1.0.0"
  },
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
```

---

## 🔌 Connect to Claude Desktop

```json
{
  "mcpServers": {
    "qa-tools": {
      "command": "node",
      "args": ["/path/to/qa-mcp-server/dist/index.js"]
    }
  }
}
```

---

## ✅ Test Your Server

1. Build: `npm run build`
2. Restart Claude Desktop
3. Ask: "What QA tools are available?"
4. Try: "Run tests for login.spec.ts"

---

## 📚 See Also

- [MCP Server Python](ch_05_mcp_server_python.md)
- [MCP Architecture](../mcp_fundamentals/ch_05_mcp_architecture.md)
