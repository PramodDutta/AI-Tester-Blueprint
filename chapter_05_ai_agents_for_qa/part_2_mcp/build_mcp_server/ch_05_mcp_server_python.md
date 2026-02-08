# Build MCP Server (Python)

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Build an MCP server in Python for QA automation tools.

---

## 📦 Setup

```bash
mkdir qa-mcp-python
cd qa-mcp-python
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install mcp
```

---

## 📝 Basic Server

```python
# server.py
import subprocess
import json
from mcp.server import Server
from mcp.server.stdio import stdio_server
from mcp.types import Tool, TextContent

# Create server
server = Server("qa-tools")

@server.list_tools()
async def list_tools():
    """List available QA tools."""
    return [
        Tool(
            name="run_pytest",
            description="Run pytest tests",
            inputSchema={
                "type": "object",
                "properties": {
                    "test_path": {
                        "type": "string",
                        "description": "Path to test file or directory"
                    },
                    "verbose": {
                        "type": "boolean",
                        "description": "Enable verbose output",
                        "default": False
                    }
                },
                "required": ["test_path"]
            }
        ),
        Tool(
            name="analyze_coverage",
            description="Analyze test coverage",
            inputSchema={
                "type": "object",
                "properties": {
                    "path": {
                        "type": "string",
                        "description": "Path to analyze"
                    }
                },
                "required": ["path"]
            }
        ),
        Tool(
            name="create_jira_bug",
            description="Create a bug ticket in Jira",
            inputSchema={
                "type": "object",
                "properties": {
                    "title": {"type": "string"},
                    "description": {"type": "string"},
                    "priority": {"type": "string", "enum": ["P0", "P1", "P2", "P3"]}
                },
                "required": ["title", "description"]
            }
        )
    ]


@server.call_tool()
async def call_tool(name: str, arguments: dict):
    """Handle tool calls."""
    
    if name == "run_pytest":
        test_path = arguments["test_path"]
        verbose = arguments.get("verbose", False)
        
        cmd = ["pytest", test_path]
        if verbose:
            cmd.append("-v")
        
        try:
            result = subprocess.run(
                cmd,
                capture_output=True,
                text=True,
                timeout=300
            )
            output = result.stdout + result.stderr
            return [TextContent(type="text", text=output)]
        except subprocess.TimeoutExpired:
            return [TextContent(type="text", text="Test execution timed out")]
        except Exception as e:
            return [TextContent(type="text", text=f"Error: {str(e)}")]
    
    elif name == "analyze_coverage":
        path = arguments["path"]
        try:
            result = subprocess.run(
                ["coverage", "report", "--include", f"{path}/*"],
                capture_output=True,
                text=True
            )
            return [TextContent(type="text", text=result.stdout)]
        except Exception as e:
            return [TextContent(type="text", text=f"Error: {str(e)}")]
    
    elif name == "create_jira_bug":
        # Example: Would integrate with Jira API
        title = arguments["title"]
        description = arguments["description"]
        priority = arguments.get("priority", "P2")
        
        # Simulate Jira creation
        ticket_id = f"BUG-{hash(title) % 10000}"
        return [TextContent(
            type="text",
            text=f"Created Jira ticket: {ticket_id}\nTitle: {title}\nPriority: {priority}"
        )]
    
    else:
        raise ValueError(f"Unknown tool: {name}")


async def main():
    """Run the MCP server."""
    async with stdio_server() as (read_stream, write_stream):
        await server.run(read_stream, write_stream)


if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

---

## 🔌 Connect to Claude Desktop

```json
{
  "mcpServers": {
    "qa-python": {
      "command": "python",
      "args": ["/path/to/qa-mcp-python/server.py"]
    }
  }
}
```

---

## ✅ Test Your Server

1. Restart Claude Desktop
2. Ask: "What test tools do you have?"
3. Try: "Run pytest on tests/test_login.py"

---

## 📚 See Also

- [MCP Server JS](ch_05_mcp_server_js.md)
- [MCP Architecture](../mcp_fundamentals/ch_05_mcp_architecture.md)
