# Write Your First QA-Style Prompt

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Hands-on guide to creating your first production-ready QA prompt
**Chapter:** 2 - Prompt Engineering

---

## Goal

By the end of this guide, you will write a complete, professional QA prompt that generates reliable test cases.

---

## Step 1: Start with a Bad Prompt

Let's start with what most people write:

```
❌ BAD PROMPT:
Write test cases for login.
```

**Problems:**
- No context
- No format
- No constraints
- Will produce inconsistent results

---

## Step 2: Add Role

```
ROLE: You are a Senior QA Engineer with 10 years of experience.

Write test cases for login.
```

**Improvement:** AI now has expertise context.

---

## Step 3: Add Context

```
ROLE: You are a Senior QA Engineer with 10 years of experience.

CONTEXT:
- Application: E-commerce website
- Login method: Email + Password
- Features: Remember me checkbox, Forgot password link

Write test cases for login.
```

**Improvement:** AI understands the specific system.

---

## Step 4: Add Task Specificity

```
ROLE: You are a Senior QA Engineer with 10 years of experience.

CONTEXT:
- Application: E-commerce website
- Login method: Email + Password
- Features: Remember me checkbox, Forgot password link

TASK:
Generate 10 test cases covering:
- 3 positive scenarios (happy path)
- 5 negative scenarios (validation errors)
- 2 security scenarios
```

**Improvement:** Clear, quantified expectations.

---

## Step 5: Add Constraints (Critical!)

```
ROLE: You are a Senior QA Engineer with 10 years of experience.

CONTEXT:
- Application: E-commerce website
- Login method: Email + Password
- Features: Remember me checkbox, Forgot password link

TASK:
Generate 10 test cases covering:
- 3 positive scenarios (happy path)
- 5 negative scenarios (validation errors)
- 2 security scenarios

CONSTRAINTS:
- Use ONLY the features mentioned above
- Do NOT assume password complexity rules (not provided)
- Do NOT invent error messages
- Mark assumptions as "[ASSUMPTION]"
```

**Improvement:** Prevents hallucinations.

---

## Step 6: Add Output Format

```
ROLE: You are a Senior QA Engineer with 10 years of experience.

CONTEXT:
- Application: E-commerce website
- Login method: Email + Password
- Features: Remember me checkbox, Forgot password link

TASK:
Generate 10 test cases covering:
- 3 positive scenarios (happy path)
- 5 negative scenarios (validation errors)
- 2 security scenarios

CONSTRAINTS:
- Use ONLY the features mentioned above
- Do NOT assume password complexity rules (not provided)
- Do NOT invent error messages
- Mark assumptions as "[ASSUMPTION]"

OUTPUT FORMAT:
| TC_ID | Category | Description | Pre-condition | Steps | Expected Result | Priority |
```

**Improvement:** Output is immediately usable.

---

## Final: Complete QA Prompt ✅

```
ROLE: 
You are a Senior QA Engineer with 10 years of experience 
in functional and security testing.

CONTEXT:
- Application: E-commerce website
- Login method: Email + Password
- Features: Remember me checkbox, Forgot password link
- Validation: Email must be valid format

TASK:
Generate exactly 10 test cases covering:
- 3 positive scenarios (successful login)
- 5 negative scenarios (validation errors)
- 2 security scenarios (SQL injection, brute force)

CONSTRAINTS:
- Use ONLY the features mentioned above
- Do NOT assume password complexity rules
- Do NOT invent error messages
- Mark any assumptions as "[ASSUMPTION]"
- If information is missing, state "Not specified"

OUTPUT FORMAT:
| TC_ID | Category | Description | Pre-condition | Steps | Expected Result | Priority |

Use TC_001, TC_002, etc. for IDs.
Priority: High / Medium / Low
```

---

## Your Turn: Practice Exercise

**Scenario:** You need to test a "Add to Cart" feature.

**Given Information:**
- Users can add products to cart
- Maximum 10 items per product
- Cart shows total price

**Your Task:**
Write a complete QA prompt using the RICE POT framework.

```
YOUR PROMPT HERE:
_________________________________________________
_________________________________________________
_________________________________________________
```

---

## Checklist: Is Your Prompt Complete?

- [ ] Role defined
- [ ] Context provided
- [ ] Task is specific and quantified
- [ ] Constraints prevent hallucinations
- [ ] Output format specified
- [ ] Terminology defined if needed

---

## See Also

- [RICE POT Framework](../core_concepts/ch_02_rice_pot_framework.md)
- [Steps for Effective Prompting](../core_concepts/ch_02_steps_effective_prompting.md)
- [Test Case Prompts](../templates/ch_02_test_case_prompts.md)

