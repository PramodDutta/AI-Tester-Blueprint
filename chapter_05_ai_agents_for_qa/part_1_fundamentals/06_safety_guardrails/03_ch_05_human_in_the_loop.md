# Human-in-the-Loop

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is Human-in-the-Loop (HITL)?

A pattern where agents pause for human approval before taking certain actions.

---

## 🔄 HITL Workflow

```
Agent: "I analyzed the requirements and want to create 15 test cases"
       [PENDING APPROVAL]
       
Human: [Review] → [Approve] / [Modify] / [Reject]

Agent: [Continues based on decision]
```

---

## 📋 When to Require Approval

| Action | Require HITL? | Why |
|--------|---------------|-----|
| Read files | No | Non-destructive |
| Write test files | Maybe | Depends on scope |
| Delete files | Yes | Destructive |
| Create Jira tickets | Yes | External visibility |
| Send Slack messages | Yes | Communication |
| Run tests | No | Usually safe |
| Modify production | Always Yes | Critical |

---

## 🛠️ Implementation Pattern

```python
def agent_action(action_type, payload):
    if requires_approval(action_type):
        approval = request_human_approval(
            action=action_type,
            details=payload,
            timeout=300  # 5 min timeout
        )
        if not approval.approved:
            return {"status": "rejected", "reason": approval.reason}
    
    # Execute action
    return execute(action_type, payload)
```

---

## 📝 Best Practices

1. **Batch approvals** — Group related actions
2. **Clear context** — Show what and why
3. **Timeouts** — Don't block forever
4. **Override options** — Allow "approve all similar"
5. **Audit trail** — Log who approved what

---

## 📚 See Also

- [Safety Fundamentals](ch_05_safety_fundamentals.md)
- [Error Handling](ch_05_error_handling.md)
