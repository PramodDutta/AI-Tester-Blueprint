# Audit Logging

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Track everything agents do for debugging, security, and compliance.

---

## 📋 What to Log

| Event | Data |
|-------|------|
| **Agent start** | Task, user, timestamp |
| **Tool call** | Tool name, parameters, result |
| **LLM request** | Prompt, response, tokens |
| **Decision** | Reasoning, chosen action |
| **Error** | Type, message, stack trace |
| **Agent end** | Status, duration, cost |

---

## 📝 Log Format

```json
{
  "timestamp": "2024-01-15T10:30:45Z",
  "agent_id": "qa-agent-01",
  "session_id": "sess_abc123",
  "event_type": "tool_call",
  "event_data": {
    "tool": "create_jira_issue",
    "params": {"title": "Login bug", "priority": "High"},
    "result": {"ticket_id": "BUG-456", "status": "created"},
    "duration_ms": 1250
  }
}
```

---

## 🗄️ Storage Options

| Option | Use Case |
|--------|----------|
| File logs | Simple, local |
| Database | Searchable |
| Cloud logging | Production scale |
| SIEM | Security focus |

---

## 📚 See Also

- [Safety Fundamentals](ch_05_safety_fundamentals.md)
- [Agent Observability](../../part_4_advanced/advanced_topics/ch_05_agent_observability.md)
