# Few-Shot Prompting

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Learning from examples
**Chapter:** 2 - Prompt Engineering

---

## Definition

**Few-Shot Prompting** provides the model with 1-5 examples of the desired input-output pattern before asking it to perform the task.

---

## When to Use

✅ **Good for:**
- Custom output formats
- Domain-specific terminology
- Consistent style across outputs
- Complex or unusual tasks

❌ **Avoid when:**
- Simple, standard tasks (use zero-shot)
- Token limit is a concern
- Examples are hard to create

---

## Structure

```
[Optional: Role]
[Task description]

EXAMPLES:
[Input 1] → [Output 1]
[Input 2] → [Output 2]

NOW:
[Your actual input]
```

---

## QA Examples

### Example 1: Test Case Format (1-shot)

```
Generate test cases following this format:

EXAMPLE:
| TC_001 | Valid Login | Pre: User exists | 1. Enter email 2. Enter password 3. Click login | Dashboard displayed | High |

NOW GENERATE:
5 test cases for password reset functionality.
```

### Example 2: Bug Report Classification (2-shot)

```
Classify bugs by severity based on these examples:

EXAMPLE 1:
Bug: "App crashes on startup"
Classification: Critical - Complete system failure

EXAMPLE 2:
Bug: "Typo in footer text"
Classification: Low - Cosmetic issue only

NOW CLASSIFY:
Bug: "Payment fails for orders over $10,000"
```

### Example 3: API Test Generation (3-shot)

```
Generate API test cases following these examples:

EXAMPLE 1:
Endpoint: POST /users
Test: Create user with valid data
Expected: 201 Created, user object returned

EXAMPLE 2:
Endpoint: POST /users
Test: Create user with missing email
Expected: 400 Bad Request, validation error

EXAMPLE 3:
Endpoint: POST /users
Test: Create user with duplicate email
Expected: 409 Conflict, error message

NOW GENERATE:
5 test cases for DELETE /users/{id} endpoint
```

---

## How Many Examples?

| Examples | Use Case |
|----------|----------|
| 1 (one-shot) | Simple format demonstration |
| 2-3 | Standard tasks with custom format |
| 4-5 | Complex tasks or unusual patterns |

**Rule of thumb:** Use the minimum examples needed for consistency.

---

## Tips for Effective Few-Shot Prompts

1. **Diverse examples** - Cover different scenarios
2. **Consistent format** - All examples follow same structure
3. **Representative** - Examples match real use cases
4. **Clear separation** - Distinguish examples from actual task

---

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Inconsistent examples | Confused model | Use uniform format |
| Too many examples | Token waste, confusion | Limit to 3-5 |
| Poor examples | Bad outputs | Use high-quality examples |
| No separator | Model continues examples | Add "NOW:" or clear break |

---

## See Also

- [Zero-Shot Prompting](ch_02_zero_shot_prompting.md)
- [Chain-of-Thought](ch_02_chain_of_thought.md)
- [Test Case Prompts](../templates/ch_02_test_case_prompts.md)

