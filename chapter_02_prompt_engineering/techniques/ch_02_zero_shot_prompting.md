# Zero-Shot Prompting

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Direct instructions without examples
**Chapter:** 2 - Prompt Engineering

---

## Definition

**Zero-Shot Prompting** means giving the model a task without providing any examples. The model relies entirely on its training to understand and complete the task.

---

## When to Use

✅ **Good for:**
- Simple, well-defined tasks
- Standard formats (JSON, tables, lists)
- Quick iterations and exploration
- When you trust the model's default behavior

❌ **Avoid when:**
- Custom output format required
- Domain-specific terminology needed
- High consistency across outputs required

---

## Structure

```
[Optional: Role]
[Task description]
[Optional: Constraints]
[Optional: Format specification]
```

---

## QA Examples

### Example 1: Basic Test Case Generation

```
Generate 5 test cases for a password reset feature.
Include: Test ID, Description, Steps, Expected Result.
```

### Example 2: With Role and Constraints

```
ROLE: You are a QA Engineer.

TASK: Generate negative test cases for an email input field.

CONSTRAINTS:
- Focus on validation errors
- Include boundary cases
- Do not include SQL injection (covered separately)

FORMAT: Bullet list with description and expected error message.
```

### Example 3: Bug Classification

```
Classify this bug report by severity (Critical/High/Medium/Low):

"Users cannot complete checkout when cart has more than 50 items. 
Error 500 is displayed."

Provide: Severity, Justification, Recommended Priority.
```

---

## Tips for Effective Zero-Shot Prompts

| Tip | Example |
|-----|---------|
| Be specific | "5 test cases" not "some test cases" |
| Define scope | "for login feature" not "for the app" |
| Specify format | "as a table" or "as JSON" |
| Add constraints | "do not assume..." |

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Too vague | Inconsistent outputs | Add specific details |
| No format | Unstructured response | Specify output format |
| No constraints | Hallucinations | Add anti-hallucination rules |

---

## See Also

- [Few-Shot Prompting](ch_02_few_shot_prompting.md)
- [Chain-of-Thought](ch_02_chain_of_thought.md)
- [Prompt Types](../core_concepts/ch_02_prompt_types.md)

