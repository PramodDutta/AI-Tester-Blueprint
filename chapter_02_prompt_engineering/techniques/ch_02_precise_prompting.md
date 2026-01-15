# Precise Prompting

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Writing highly specific prompts for accurate outputs
**Chapter:** 2 - Prompt Engineering

---

## What is Precise Prompting?

**Precise Prompting** is the practice of writing highly specific, unambiguous prompts that leave no room for interpretation, resulting in consistent, accurate outputs.

---

## Zero-Shot vs Precise Prompting

| Aspect | Zero-Shot | Precise Prompting |
|--------|-----------|-------------------|
| **Examples** | None | None (but highly detailed) |
| **Specificity** | General | Extremely detailed |
| **Output consistency** | Variable | Highly consistent |
| **Token usage** | Low | Medium |
| **Best for** | Quick tasks | Critical/production tasks |

---

## The Precision Spectrum

```
VAGUE ←─────────────────────────────────────→ PRECISE

"Write tests"     "Write 5 login     "Write exactly 5 functional
                   test cases"        test cases for email/password
                                      login covering: valid login,
                                      invalid email format, wrong
                                      password, empty fields, and
                                      SQL injection attempt. Use
                                      format: ID | Description |
                                      Steps | Expected | Priority"
```

---

## Precision Techniques

### 1. Quantify Everything

```
❌ Vague: "Generate some test cases"
✅ Precise: "Generate exactly 10 test cases"

❌ Vague: "Include important scenarios"
✅ Precise: "Include 3 positive and 7 negative scenarios"
```

### 2. Name Specific Scenarios

```
❌ Vague: "Cover edge cases"
✅ Precise: "Cover these edge cases:
   - Empty string input
   - Maximum length (255 characters)
   - Special characters (!@#$%)
   - Unicode characters
   - Leading/trailing spaces"
```

### 3. Define Exact Format

```
❌ Vague: "Return as a table"
✅ Precise: "Return in this exact format:
   | Test ID | Category | Description | Pre-condition | Steps | Expected Result | Priority |
   Use TC_XXX format for Test ID. Priority must be High/Medium/Low."
```

### 4. Specify What NOT to Include

```
❌ Missing: (no exclusions)
✅ Precise: "Do NOT include:
   - Performance test cases
   - Security test cases (covered separately)
   - UI/UX validation
   - Browser compatibility"
```

### 5. Define Terminology

```
❌ Ambiguous: "Test the happy path"
✅ Precise: "Test the happy path, defined as:
   - Valid user credentials
   - Active account status
   - Successful authentication
   - Redirect to dashboard"
```

---

## Precise Prompting Template

```
TASK: [Exactly what to do]

QUANTITY: [Exact numbers]
- [X] items of type A
- [Y] items of type B

MUST INCLUDE:
- [Specific item 1]
- [Specific item 2]
- [Specific item 3]

MUST EXCLUDE:
- [What to skip 1]
- [What to skip 2]

FORMAT:
[Exact structure with column names/fields]

DEFINITIONS:
- Term A = [Definition]
- Term B = [Definition]

CONSTRAINTS:
- [Rule 1]
- [Rule 2]
```

---

## Example: Vague vs Precise

### ❌ Vague Prompt
```
Write test cases for user registration.
```

### ✅ Precise Prompt
```
TASK: Generate exactly 8 test cases for user registration.

FIELDS TO TEST:
- Email (required, valid format)
- Password (required, min 8 chars, 1 uppercase, 1 number)
- Confirm Password (must match)
- Terms checkbox (required)

MUST INCLUDE:
- 2 positive scenarios (successful registration)
- 3 validation error scenarios
- 2 boundary value scenarios
- 1 duplicate email scenario

MUST EXCLUDE:
- Social login (covered separately)
- Email verification flow

FORMAT:
| TC_ID | Type | Field | Input | Expected Result |

CONSTRAINTS:
- Use realistic but fictional test data
- Do NOT assume validation rules not listed above
```

---

## When to Use Precise Prompting

| Use Precise Prompting | Use Zero-Shot |
|----------------------|---------------|
| Production test cases | Quick exploration |
| Audit/compliance docs | Brainstorming |
| Automated test scripts | Initial drafts |
| Client deliverables | Internal notes |
| Critical bug analysis | Quick questions |

---

## See Also

- [Zero-Shot Prompting](ch_02_zero_shot_prompting.md)
- [Few-Shot Prompting](ch_02_few_shot_prompting.md)
- [RICE POT Framework](../core_concepts/ch_02_rice_pot_framework.md)

