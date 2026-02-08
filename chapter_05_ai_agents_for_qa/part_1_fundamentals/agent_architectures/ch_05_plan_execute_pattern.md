# Plan-Execute Pattern

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is Plan-Execute?

A two-phase approach: First plan all steps, then execute them sequentially.

---

## 🔄 The Pattern

```
┌─────────────────────────────────────────────────────┐
│               PLAN-EXECUTE PATTERN                   │
└─────────────────────────────────────────────────────┘

         PHASE 1: PLAN                PHASE 2: EXECUTE
         ─────────────                ────────────────
    ┌─────────────────┐         ┌─────────────────────┐
    │ Analyze Goal    │         │ Step 1: Read spec   │
    │      ↓          │         │      ↓              │
    │ Decompose Tasks │   →     │ Step 2: Write tests │
    │      ↓          │         │      ↓              │
    │ Create Plan     │         │ Step 3: Run tests   │
    │      ↓          │         │      ↓              │
    │ Output Steps    │         │ Step 4: Report      │
    └─────────────────┘         └─────────────────────┘
```

---

## 📝 Example

```
Goal: "Set up API testing for the payment module"

PLAN PHASE:
Plan:
1. Read payment API documentation
2. Identify all endpoints
3. Create test cases for each endpoint
4. Generate pytest fixtures
5. Write test files
6. Configure CI/CD
7. Run tests and report

EXECUTE PHASE:
[Executing Step 1...] → Done
[Executing Step 2...] → Found 8 endpoints
[Executing Step 3...] → Created 24 test cases
...
```

---

## ✅ When to Use

| ✅ Good For | ❌ Not Great For |
|-------------|------------------|
| Complex multi-step tasks | Simple tasks |
| Clear dependencies | Exploratory work |
| Predictable workflows | Uncertain outcomes |
| Batch operations | Interactive tasks |

---

## 🎯 QA Applications

- Full test suite setup
- Migration projects
- CI/CD configuration
- Documentation generation

---

## 📚 See Also

- [ReAct Pattern](ch_05_react_pattern.md)
- [Choosing Architecture](ch_05_choosing_architecture.md)
