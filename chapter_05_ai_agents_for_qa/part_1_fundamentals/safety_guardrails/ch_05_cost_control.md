# Cost Control

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Agents can consume significant API costs. Implement cost controls to prevent budget overruns.

---

## 💰 Cost Factors

| Factor | Impact | Control Strategy |
|--------|--------|------------------|
| **Token usage** | High | Limit context size |
| **API calls** | Medium | Cache, batch |
| **Model choice** | High | Use cheaper models for simple tasks |
| **Retries** | Medium | Limit retry count |

---

## 📊 Model Cost Comparison

| Model | Input (1M tokens) | Output (1M tokens) | Use For |
|-------|-------------------|--------------------| --------|
| GPT-4o | $2.50 | $10.00 | Complex reasoning |
| GPT-4o-mini | $0.15 | $0.60 | Most tasks |
| Claude 3 Opus | $15.00 | $75.00 | Critical tasks |
| Claude 3 Sonnet | $3.00 | $15.00 | Balanced |
| Claude 3 Haiku | $0.25 | $1.25 | High volume |

---

## 🛠️ Cost Control Strategies

### 1. Token Budgets
```python
MAX_TOKENS_PER_TASK = 50000
MAX_TOKENS_PER_DAY = 1000000

if current_usage > MAX_TOKENS_PER_DAY:
    raise BudgetExceeded("Daily token limit reached")
```

### 2. Model Tiering
```
Simple tasks → GPT-4o-mini (cheap)
Complex reasoning → GPT-4o (medium)
Critical decisions → Claude Opus (expensive, but worth it)
```

### 3. Caching
```python
@cache(ttl=3600)
def analyze_requirements(req_file):
    # Don't re-analyze same file twice
    return agent.analyze(req_file)
```

### 4. Batching
```
❌ 100 separate API calls
✅ 1 batched API call with 100 items
```

---

## 📈 Monitoring

Track these metrics:
- Tokens per task
- Cost per agent run
- Daily/weekly/monthly spend
- Cost per test generated

---

## 📚 See Also

- [Safety Fundamentals](ch_05_safety_fundamentals.md)
- [Agent Evaluation](../agent_evaluation/ch_05_efficiency_metrics.md)
