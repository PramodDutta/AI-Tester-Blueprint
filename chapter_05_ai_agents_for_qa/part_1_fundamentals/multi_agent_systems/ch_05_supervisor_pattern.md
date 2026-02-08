# Supervisor Pattern

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is the Supervisor Pattern?

A central agent (supervisor) coordinates multiple worker agents, delegating tasks and aggregating results.

---

## 🔄 How It Works

```
User Request
     │
     ▼
┌─────────────────────────────────────────────┐
│            SUPERVISOR AGENT                  │
│                                             │
│  1. Analyze request                         │
│  2. Break into subtasks                     │
│  3. Delegate to workers                     │
│  4. Collect results                         │
│  5. Synthesize final output                 │
└───────────────┬─────────────────────────────┘
        ┌───────┼───────┐
        ▼       ▼       ▼
    ┌───────┐┌───────┐┌───────┐
    │Worker ││Worker ││Worker │
    │   1   ││   2   ││   3   │
    └───────┘└───────┘└───────┘
```

---

## 📝 QA Example: Test Suite Generator

```python
# Supervisor Agent
class TestSupervisor:
    def __init__(self):
        self.workers = {
            "requirements": RequirementsAnalyzer(),
            "test_writer": TestCaseWriter(),
            "code_gen": CodeGenerator(),
            "reviewer": TestReviewer()
        }
    
    def generate_test_suite(self, prd_file):
        # Step 1: Analyze requirements
        reqs = self.workers["requirements"].analyze(prd_file)
        
        # Step 2: Generate test cases
        test_cases = self.workers["test_writer"].create(reqs)
        
        # Step 3: Generate code
        code = self.workers["code_gen"].generate(test_cases)
        
        # Step 4: Review
        review = self.workers["reviewer"].review(code)
        
        return {
            "test_cases": test_cases,
            "code": code,
            "review": review
        }
```

---

## ✅ When to Use

- Complex multi-step workflows
- Need centralized control
- Different specialists required
- Results need aggregation

---

## 📚 See Also

- [Multi-Agent Overview](ch_05_multi_agent_overview.md)
- [Hierarchical Pattern](ch_05_hierarchical_pattern.md)
