# Error Handling

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Agents will fail. Proper error handling prevents cascading failures.

---

## 📋 Common Agent Failures

| Failure Type | Cause | Mitigation |
|--------------|-------|------------|
| **Tool failure** | API down, timeout | Retry with backoff |
| **Invalid output** | LLM generates bad JSON | Parse validation |
| **Infinite loop** | Agent stuck on task | Max iterations |
| **Hallucination** | Wrong information | Validation checks |
| **Rate limit** | Too many requests | Throttling |

---

## 🔄 Error Handling Patterns

### Retry with Backoff

```python
def call_with_retry(func, max_retries=3):
    for attempt in range(max_retries):
        try:
            return func()
        except RetryableError:
            wait = 2 ** attempt  # 1, 2, 4 seconds
            time.sleep(wait)
    raise MaxRetriesExceeded()
```

### Graceful Degradation

```
Primary: Use Claude API → Failed
Fallback 1: Use GPT-4 → Failed
Fallback 2: Use local Ollama → Success ✓
```

### Circuit Breaker

```
If >5 failures in 1 minute:
  Stop calling that service
  Wait 5 minutes
  Try again
```

---

## 🛠️ Implementation Checklist

- [ ] All tool calls have try/catch
- [ ] Timeouts on all external calls
- [ ] Max iteration limits on loops
- [ ] Fallback strategies defined
- [ ] Error logging enabled
- [ ] Alert on repeated failures

---

## 📚 See Also

- [Safety Fundamentals](ch_05_safety_fundamentals.md)
- [Cost Control](ch_05_cost_control.md)
