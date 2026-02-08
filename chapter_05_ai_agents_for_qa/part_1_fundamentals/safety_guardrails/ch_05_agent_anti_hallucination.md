# Agent Anti-Hallucination

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Agents inherit LLM hallucination risks AND add new risks from autonomous action. This guide extends Chapter 1's anti-hallucination rules for agents.

---

## ⚠️ Agent-Specific Hallucination Risks

| Risk | Example | Consequence |
|------|---------|-------------|
| **Fake tool results** | Agent claims file was read but wasn't | Wrong decisions |
| **Invented APIs** | Agent tries to call non-existent endpoint | Failures |
| **False completion** | Agent says task done when it isn't | Unfinished work |
| **Made-up data** | Agent generates fake test results | False confidence |
| **Imagined context** | Agent assumes things not verified | Wrong actions |

---

## ✅ Anti-Hallucination Rules for Agents

### Rule 1: Verify Tool Outputs
```
❌ Agent: "I read the file and it says X"
✅ Agent: [Shows actual file content] "The file contains X"
```

### Rule 2: Confirm Before Acting
```
❌ Agent: "I'll delete the old tests" [deletes]
✅ Agent: "I found 50 old tests. Should I delete them?" [waits]
```

### Rule 3: Ground in Evidence
```
❌ Agent: "Based on best practices, do X"
✅ Agent: "Based on your team's test-patterns.md, do X"
```

### Rule 4: Admit Uncertainty
```
❌ Agent: "The bug is in the auth module"
✅ Agent: "Based on the error, the bug might be in auth, 
          but I need to verify by checking logs"
```

### Rule 5: Validate Completeness
```
❌ Agent: "All tests passing" (checked 5 of 100)
✅ Agent: "Ran 100 tests, all passing"
```

---

## 🛡️ Implementation Strategies

| Strategy | How It Works |
|----------|--------------|
| **Output validation** | Check tool returns match expected format |
| **Checksums** | Verify file contents weren't imagined |
| **Assertion checks** | Validate agent claims against reality |
| **Human spot-checks** | Randomly verify agent outputs |

---

## 📝 Key Takeaway

> **Trust but verify.** Agents are powerful but imperfect. Build verification into your workflows.

---

## 📚 See Also

- [Chapter 1: Anti-Hallucination Rules](../../../chapter_01_foundation_model/rules_checklists/ch_01_anti_hallucination.md)
- [Safety Fundamentals](ch_05_safety_fundamentals.md)
