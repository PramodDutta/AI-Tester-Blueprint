# OODA Loop

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is OODA?

OODA = **O**bserve → **O**rient → **D**ecide → **A**ct

Originally a military concept, now applied to real-time AI systems.

---

## 🔄 The Loop

```
     ┌─────────────────────────────────────────┐
     │              OODA LOOP                   │
     └─────────────────────────────────────────┘

        ┌──────────┐      ┌──────────┐
        │ OBSERVE  │ ───► │  ORIENT  │
        │          │      │          │
        │ Gather   │      │ Analyze  │
        │ data     │      │ context  │
        └──────────┘      └────┬─────┘
             ▲                 │
             │                 ▼
        ┌────┴─────┐      ┌──────────┐
        │   ACT    │ ◄─── │  DECIDE  │
        │          │      │          │
        │ Execute  │      │ Choose   │
        │ action   │      │ action   │
        └──────────┘      └──────────┘
```

---

## 📝 QA Example

```
OBSERVE: Test failure detected in CI pipeline
ORIENT:  Analyze error logs, check recent commits
DECIDE:  Rerun test or escalate based on pattern
ACT:     Execute chosen action

(Loop continues monitoring)
```

---

## ✅ When to Use

- Real-time monitoring
- CI/CD integration
- Live incident response
- Continuous testing

---

## 📚 See Also

- [Architecture Overview](ch_05_architecture_overview.md)
