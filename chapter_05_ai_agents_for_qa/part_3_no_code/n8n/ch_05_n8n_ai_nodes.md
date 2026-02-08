# n8n AI Nodes

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

n8n has powerful AI nodes for building intelligent automations.

---

## 🧩 Core AI Nodes

### 1. AI Agent

The most powerful node — an autonomous agent with tools.

```
┌─────────────────────────────────────────┐
│              AI AGENT                    │
│                                          │
│  LLM: Claude 3 / GPT-4                  │
│  Tools:                                  │
│    - HTTP Request Tool                  │
│    - Code Tool                          │
│    - Calculator                         │
│  Memory: Window Memory (10 messages)    │
│                                          │
│  System Prompt:                         │
│  "You are a QA assistant..."            │
└─────────────────────────────────────────┘
```

**Use Case:** Complex multi-step QA tasks

### 2. Basic LLM Chain

Simple prompt → response flow.

```
Input → LLM → Output
```

**Use Case:** Text generation, analysis

### 3. Summarization Chain

Summarize long content.

**Use Case:** Test report summaries

### 4. Question & Answer Chain

RAG-enabled Q&A over documents.

**Use Case:** QA knowledge base queries

---

## 🔧 AI Agent Configuration

### System Prompt for QA Agent

```
You are a QA Automation Agent. Your capabilities:

1. Analyze test requirements
2. Generate test cases  
3. Review test code
4. Suggest improvements
5. Create bug reports

Rules:
- Always be specific with test steps
- Include expected results
- Prioritize edge cases
- Follow company testing standards
```

### Adding Tools

1. **HTTP Request Tool:** Call external APIs
2. **Code Tool:** Execute JavaScript
3. **Calculator:** Math operations
4. **Jira Tool:** Create/update tickets

---

## 📊 Memory Options

| Memory Type | Use Case |
|-------------|----------|
| **Window Memory** | Keep last N messages |
| **Buffer Memory** | Full conversation |
| **Summary Memory** | Compressed history |
| **Vector Store** | Long-term retrieval |

---

## 💡 Example: Test Case Generator

```
[Webhook] → [AI Agent] → [Jira]

AI Agent Config:
- Model: Claude 3.5 Sonnet
- System: "Generate test cases from requirements"
- Tools: HTTP Request (for fetching docs)
```

---

## 📚 See Also

- [n8n Setup](ch_05_n8n_setup.md)
- [Test Plan Generator Project](ch_05_n8n_test_plan_generator.md)
