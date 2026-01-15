# Chain-of-Thought Prompting

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Step-by-step reasoning for complex tasks
**Chapter:** 2 - Prompt Engineering

---

## Definition

**Chain-of-Thought (CoT) Prompting** instructs the model to break down complex problems into intermediate reasoning steps before arriving at a final answer.

---

## When to Use

✅ **Good for:**
- Complex analysis tasks
- Multi-step problems
- When reasoning transparency matters
- Debugging or root cause analysis
- Test coverage analysis

❌ **Avoid when:**
- Simple, direct tasks
- Token efficiency is critical
- Speed is priority over accuracy

---

## Structure

```
[Task description]

Think through this step by step:
Step 1: [First analysis step]
Step 2: [Second analysis step]
Step 3: [Continue as needed]
Final: [Conclusion/Output]
```

---

## QA Examples

### Example 1: Bug Analysis

```
Analyze this bug report step by step:

Step 1: Identify the reported symptoms
Step 2: List possible root causes
Step 3: Determine what information is missing
Step 4: Suggest debugging steps
Step 5: Recommend severity classification

Bug Report:
"Checkout fails intermittently on mobile devices during peak hours.
Users see a spinning loader that never completes."
```

### Example 2: Test Coverage Review

```
Review this test suite for coverage gaps:

Step 1: List all features mentioned in the PRD
Step 2: Map existing tests to features
Step 3: Identify untested features
Step 4: Identify missing edge cases
Step 5: Prioritize gaps by risk

PRD: [paste PRD]
Test Cases: [paste test cases]
```

### Example 3: Requirements Analysis

```
Analyze this requirement for testability:

Step 1: Extract explicit requirements
Step 2: Identify implicit assumptions
Step 3: List ambiguous statements
Step 4: Determine missing acceptance criteria
Step 5: Generate clarification questions

Requirement:
"Users should be able to easily search for products"
```

---

## Magic Phrase: "Let's think step by step"

Simply adding this phrase can trigger CoT behavior:

```
Determine if this test case is complete. Let's think step by step.

Test Case: "Verify login works with valid credentials"
```

---

## CoT with Examples (CoT Few-Shot)

Combine CoT with examples for best results:

```
EXAMPLE:
Requirement: "Password must be strong"
Step 1: "Strong" is subjective - needs definition
Step 2: Missing: minimum length, character requirements
Step 3: Missing: error messages for weak passwords
Conclusion: Requirement is incomplete, needs clarification

NOW ANALYZE:
Requirement: "System should be fast"
```

---

## Tips for Effective CoT Prompts

| Tip | Why |
|-----|-----|
| Number your steps | Clearer structure |
| Be specific about each step | Better reasoning |
| Ask for final conclusion | Ensures actionable output |
| Limit steps (3-7) | Prevents rambling |

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Too many steps | Verbose, unfocused | Limit to 5-7 steps |
| Vague steps | Shallow analysis | Make steps specific |
| No conclusion | Missing actionable output | Add "Final:" step |

---

## See Also

- [Zero-Shot Prompting](ch_02_zero_shot_prompting.md)
- [Few-Shot Prompting](ch_02_few_shot_prompting.md)
- [Bug Report Prompts](../templates/ch_02_bug_report_prompts.md)

