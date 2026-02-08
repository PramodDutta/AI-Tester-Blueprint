# Agent Actions

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Actions are the execution layer — where agents interact with the real world.

---

## 🔄 Action Lifecycle

```
Decision           Tool Call           Execution           Result
────────          ──────────          ─────────          ──────
"I need to      → run_tests()      → pytest runs      → 15 tests passed
 run tests"       invoked            actually           2 failed
```

---

## 📋 Action Types

| Type | Description | Example |
|------|-------------|---------|
| **Read** | Get information | Read file, query API |
| **Write** | Create/modify | Write file, update DB |
| **Execute** | Run something | Run tests, execute code |
| **Communicate** | Send messages | Slack, email, Jira |
| **Navigate** | Browse | Open URL, click button |

---

## 🎯 QA Action Examples

```python
# Common QA Agent Actions

# 1. Execute Tests
action = run_tests(
    test_file="tests/login_test.py",
    browser="chromium"
)

# 2. File Bug
action = create_jira_issue(
    project="QA",
    type="Bug",
    title="Login fails with special characters",
    priority="High"
)

# 3. Notify Team
action = send_slack(
    channel="#qa-alerts",
    message="Build failed: 5 tests broken"
)

# 4. Update Test
action = write_file(
    path="tests/login_test.py",
    content=updated_test_code
)
```

---

## ⚠️ Action Safety

| Risk | Mitigation |
|------|------------|
| Destructive actions | Require approval |
| Infinite loops | Max action limit |
| Wrong target | Validate before execute |
| Sensitive data | Mask credentials |

---

## 📚 See Also

- [Agent Tools](ch_05_agent_tools.md)
- [Error Handling](../safety_guardrails/ch_05_error_handling.md)
