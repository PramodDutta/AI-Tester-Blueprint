# What is an AI Agent?

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Foundational understanding of AI Agents  
**Chapter:** 5 - AI Agents for QA  
**Part:** 1 - Fundamentals

---

## 🎯 What You'll Learn

- What an AI agent is (and isn't)
- The core components of an agent
- How agents differ from simple chatbots
- Real-world examples of AI agents
- Why agents matter for QA

---

## 📖 Definition

### Simple Definition

> **AI Agent** = An AI system that can **perceive** its environment, **reason** about goals, **plan** actions, and **execute** tasks autonomously, using tools when needed.

### Technical Definition

> An AI Agent is an autonomous software entity powered by a Large Language Model (LLM) that can:
> 1. Understand natural language instructions (goals)
> 2. Break down complex tasks into steps
> 3. Use external tools (APIs, databases, browsers)
> 4. Maintain memory across interactions
> 5. Learn from feedback and outcomes

---

## 🧠 The Mental Model

Think of an AI Agent like a **smart assistant with hands**.

| Component | Human Analogy | Agent Equivalent |
|-----------|---------------|------------------|
| **Brain** | Thinking | LLM (reasoning engine) |
| **Eyes** | Seeing | Perception (reading inputs) |
| **Memory** | Remembering | Context window + external memory |
| **Hands** | Doing | Tools (APIs, code execution) |
| **Plan** | Strategy | Task decomposition |

```
┌─────────────────────────────────────────────────────────────────┐
│                        AI AGENT                                  │
│                                                                  │
│   ┌──────────┐                                                  │
│   │  BRAIN   │  ← LLM (GPT, Claude, Llama)                     │
│   │ (Reason) │                                                  │
│   └────┬─────┘                                                  │
│        │                                                        │
│   ┌────┴────┐                                                   │
│   │         │                                                   │
│   ▼         ▼                                                   │
│ ┌─────┐  ┌─────┐  ┌──────┐  ┌──────┐                          │
│ │EYES │  │ EAR │  │MEMORY│  │HANDS │                          │
│ │Read │  │Input│  │Store │  │Tools │                          │
│ └─────┘  └─────┘  └──────┘  └──────┘                          │
│                                                                  │
│         Perceive    →    Think    →    Act                      │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 The Agent Loop

Every agent runs in a continuous loop:

```
User Goal: "Create test cases for the login feature"
                        │
                        ▼
    1. PERCEIVE  → Read the goal, gather context
    2. REASON    → "I need to understand the login feature"
    3. PLAN      → Step 1: Read requirements, Step 2: Write tests
    4. ACT       → Use tool: read_file("requirements.md")
    5. OBSERVE   → Got requirements data
    6. REPEAT    → Until goal achieved
                        │
                        ▼
    Output: 10 test cases covering login scenarios
```

---

## 🎯 Real-World QA Examples

### Example 1: Test Generation Agent
```
Goal: "Write tests for checkout API"
→ Read API spec → Identify endpoints → Generate pytest code → Run tests
```

### Example 2: Bug Triage Agent
```
Goal: "Triage incoming bugs"
→ Read Jira tickets → Analyze severity → Assign to team → Notify
```

### Example 3: Self-Healing Test Agent
```
Goal: "Fix broken test"
→ Detect failure → Analyze error → Find new selector → Update code → Rerun
```

---

## 🆚 Agent vs LLM: Quick Comparison

| Aspect | LLM (ChatGPT) | AI Agent |
|--------|---------------|----------|
| **Input** | Text prompt | Goal or task |
| **Output** | Text response | Completed task |
| **Tools** | None | APIs, DBs, browsers |
| **Memory** | Context window | Short + Long-term |
| **Steps** | Single response | Multiple steps |
| **Autonomy** | User drives | Agent drives |

---

## 🧩 Core Agent Components

| Component | Purpose | QA Example |
|-----------|---------|------------|
| **LLM (Brain)** | Reasoning | Analyze requirements |
| **Memory** | Store context | Remember past test runs |
| **Planner** | Break down tasks | Create test plan |
| **Tools** | Take actions | Run Playwright tests |

---

## 📝 Key Takeaways

1. **Agent = LLM + Tools + Memory + Autonomy**
2. **Agents take real actions** (not just respond)
3. **Agents work toward goals** (multi-step)
4. **Agents remember context** (across interactions)

---

## 📚 See Also

- [Agents vs LLM](ch_05_agents_vs_llm.md)
- [Agent Components](../agent_anatomy/ch_05_agent_components.md)
- [Why Agents for QA?](ch_05_why_agents_for_qa.md)
