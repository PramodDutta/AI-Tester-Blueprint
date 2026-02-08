# Agent Tools

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What Are Agent Tools?

Tools are functions that agents can call to interact with the external world. They're what transform an LLM from a text generator into an action-taker.

> **Definition:** A tool is a function with a name, description, and parameters that an agent can invoke to perform actions.

---

## 🔧 Tool Structure

```json
{
  "name": "search_jira",
  "description": "Search Jira tickets using JQL query",
  "parameters": {
    "jql": {
      "type": "string",
      "description": "JQL query string"
    },
    "max_results": {
      "type": "integer",
      "default": 10
    }
  }
}
```

---

## 📋 Common Tool Categories

### File Operations
| Tool | Purpose |
|------|---------|
| `read_file` | Read file contents |
| `write_file` | Create/update files |
| `list_directory` | Browse folders |
| `search_files` | Find files by pattern |

### Code Execution
| Tool | Purpose |
|------|---------|
| `run_python` | Execute Python code |
| `run_shell` | Execute shell commands |
| `run_tests` | Execute test suites |

### API Interactions
| Tool | Purpose |
|------|---------|
| `http_request` | Make HTTP calls |
| `jira_api` | Interact with Jira |
| `slack_send` | Send Slack messages |
| `github_api` | GitHub operations |

### Browser Automation
| Tool | Purpose |
|------|---------|
| `navigate` | Go to URL |
| `click` | Click element |
| `type` | Enter text |
| `screenshot` | Capture screen |

### Database
| Tool | Purpose |
|------|---------|
| `query_sql` | Run SQL queries |
| `insert_record` | Add data |

---

## 🎯 QA-Specific Tools

```python
# Example QA Tool Definitions
qa_tools = [
    {
        "name": "run_playwright_test",
        "description": "Execute a Playwright test file",
        "parameters": {"test_file": "string", "headed": "boolean"}
    },
    {
        "name": "create_jira_bug",
        "description": "Create a bug ticket in Jira",
        "parameters": {"title": "string", "description": "string", "priority": "string"}
    },
    {
        "name": "get_test_results",
        "description": "Fetch test results from CI/CD",
        "parameters": {"pipeline_id": "string", "job_name": "string"}
    },
    {
        "name": "analyze_failure",
        "description": "Analyze why a test failed",
        "parameters": {"test_name": "string", "error_log": "string"}
    }
]
```

---

## 📝 Best Practices

| Practice | Why |
|----------|-----|
| **Clear descriptions** | Helps LLM choose the right tool |
| **Minimal parameters** | Less confusion for the agent |
| **Error handling** | Return clear error messages |
| **Logging** | Track what tools were called |
| **Rate limiting** | Prevent runaway execution |

---

## 📚 See Also

- [Agent Components](ch_05_agent_components.md)
- [Tool Calling](../agent_capabilities/ch_05_tool_use.md)
