# AI Agents vs LLM

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Understanding the key differences between AI Agents and LLMs  
**Chapter:** 5 - AI Agents for QA  
**Part:** 1 - Fundamentals

---

## 🎯 Overview

Many people confuse AI Agents with LLMs. While they're related, they're fundamentally different. Understanding this distinction is critical for building effective QA automation.

> **Key Insight:** An LLM is the brain. An Agent is the brain + body + tools + memory.

---

## 📊 Detailed Comparison

| Aspect | LLM | AI Agent |
|--------|-----|----------|
| **What it is** | Language model (text in → text out) | Autonomous system with tools |
| **Interaction** | Single turn or conversation | Multi-step task execution |
| **Actions** | Only generates text | Executes real actions |
| **Tools** | Cannot use tools | Uses APIs, databases, browsers |
| **Memory** | Limited to context window | Short-term + Long-term memory |
| **Autonomy** | Responds to prompts | Pursues goals independently |
| **Planning** | No planning | Decomposes tasks into steps |
| **Learning** | Static after training | Can learn from feedback |
| **Error Recovery** | Cannot retry | Can retry and adapt |

---

## 🎭 The Same Task: LLM vs Agent

### Task: "Find all P0 bugs from last week and summarize them"

**LLM Response:**
```
I don't have access to your bug tracking system. Please paste the 
bug descriptions here, and I'll summarize them for you.
```

**Agent Response:**
```
Connecting to Jira... ✓
Querying: priority = P0 AND created >= -7d... ✓
Found 8 P0 bugs

Summary:
├── Authentication: 3 bugs (BUG-101, BUG-105, BUG-108)
├── Payment: 2 bugs (BUG-102, BUG-107)
├── Performance: 2 bugs (BUG-103, BUG-106)
└── API: 1 bug (BUG-104)

Most Critical: BUG-101 - Login bypass vulnerability
Avg Resolution Time: 4.2 hours
Teams Notified: Security, Backend
```

---

## 🔄 Execution Model Comparison

### LLM: Single Turn
```
User Prompt ──────► LLM ──────► Response
                    (one step)
```

### Agent: Multi-Step Loop
```
User Goal
    │
    ▼
┌──────────────────────────────────────┐
│            AGENT LOOP                 │
│                                       │
│  ┌─────┐   ┌─────┐   ┌─────┐        │
│  │Think│ → │ Act │ → │Check│ ──┐    │
│  └─────┘   └─────┘   └─────┘   │    │
│      ▲                         │    │
│      └─────────────────────────┘    │
│            (repeat until done)       │
└──────────────────────────────────────┘
    │
    ▼
Completed Task
```

---

## 🛠️ Tool Usage: The Key Difference

### What LLMs Cannot Do

| Action | LLM | Agent |
|--------|-----|-------|
| Read a file from disk | ❌ | ✅ |
| Query a database | ❌ | ✅ |
| Make HTTP requests | ❌ | ✅ |
| Run shell commands | ❌ | ✅ |
| Browse the web | ❌ | ✅ |
| Send emails/messages | ❌ | ✅ |
| Execute code | ❌ | ✅ |
| Create/modify files | ❌ | ✅ |

### Agent Tool Example

```python
# Agent has access to tools like:
tools = [
    {
        "name": "read_jira_ticket",
        "description": "Read a Jira ticket by ID",
        "parameters": {"ticket_id": "string"}
    },
    {
        "name": "run_playwright_test",
        "description": "Execute a Playwright test file",
        "parameters": {"test_file": "string"}
    },
    {
        "name": "create_bug_report",
        "description": "Create a new bug in Jira",
        "parameters": {"title": "string", "description": "string"}
    }
]
```

---

## 🧠 Memory: Context Window vs External Memory

### LLM Memory (Limited)

```
┌─────────────────────────────────────────┐
│         CONTEXT WINDOW (128K tokens)    │
│                                         │
│  Earlier messages... │ Recent messages  │
│  (may be forgotten)  │ (remembered)     │
│                                         │
└─────────────────────────────────────────┘
```

### Agent Memory (Extended)

```
┌─────────────────────────────────────────────────┐
│                 AGENT MEMORY                     │
│                                                  │
│  ┌──────────────┐  ┌──────────────────────────┐ │
│  │ Short-Term   │  │ Long-Term                │ │
│  │ (Current     │  │ (Vector DB, Files)       │ │
│  │  session)    │  │                          │ │
│  │              │  │ • Past test results      │ │
│  │ • Current    │  │ • Known bugs             │ │
│  │   goal       │  │ • Team preferences       │ │
│  │ • Recent     │  │ • Historical patterns    │ │
│  │   actions    │  │                          │ │
│  └──────────────┘  └──────────────────────────┘ │
└─────────────────────────────────────────────────┘
```

---

## 🎯 When to Use LLM vs Agent

### Use LLM When:

- ✅ Single question/answer needed
- ✅ Text generation (no external data)
- ✅ Simple analysis of provided text
- ✅ Creative writing or brainstorming
- ✅ Code explanation or review

### Use Agent When:

- ✅ Task requires multiple steps
- ✅ Need to access external systems (Jira, DB, APIs)
- ✅ Actions must be taken (not just text generated)
- ✅ Task requires memory across sessions
- ✅ Complex workflow automation

---

## 📋 QA Use Case Matrix

| QA Task | LLM | Agent | Why |
|---------|-----|-------|-----|
| Explain test strategy | ✅ | ❌ | Text-only |
| Generate test ideas | ✅ | ❌ | Creative, no tools |
| Write tests from requirements | ⚠️ | ✅ | Agent can read files |
| Run automated tests | ❌ | ✅ | Requires execution |
| Create Jira bugs | ❌ | ✅ | Requires API |
| Analyze test results | ⚠️ | ✅ | Agent can query DB |
| Fix flaky tests | ❌ | ✅ | Multi-step, tools |
| Triage incoming bugs | ❌ | ✅ | Jira + Slack + Logic |

---

## 📝 Key Takeaways

1. **LLM = Language Model** — Generates text from text
2. **Agent = LLM + Tools + Memory + Autonomy** — Takes actions
3. **LLMs are stateless** — Agents maintain context
4. **LLMs respond** — Agents pursue goals
5. **For QA automation, you need agents** — They can actually do things

---

## 🔗 See Also

- [What is an AI Agent?](ch_05_what_is_ai_agents.md)
- [Agent Components](../agent_anatomy/ch_05_agent_components.md)
- [Agent Tools](../agent_anatomy/ch_05_agent_tools.md)
