# Anatomy of a Prompt

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Understanding the components of effective prompts
**Chapter:** 2 - Prompt Engineering

---

## The 6 Components of an Effective Prompt

```
┌─────────────────────────────────────────────────────────┐
│                    PROMPT STRUCTURE                      │
├─────────────────────────────────────────────────────────┤
│  1. ROLE        - Who should the AI be?                 │
│  2. CONTEXT     - What background information?          │
│  3. TASK        - What exactly should it do?            │
│  4. CONSTRAINTS - What rules must it follow?            │
│  5. FORMAT      - How should output be structured?      │
│  6. EXAMPLES    - What does good output look like?      │
└─────────────────────────────────────────────────────────┘
```

---

## Component Breakdown

### 1. Role (Optional but Powerful)

Assigns a persona to guide the AI's behavior.

```
ROLE: You are a Senior QA Engineer with 10+ years of experience 
in test automation and API testing.
```

**Why it works:** Sets expertise level and domain focus.

---

### 2. Context (Critical)

Provides background information the AI needs.

```
CONTEXT:
- Application: E-commerce checkout system
- Tech stack: React frontend, Node.js backend
- PRD: [paste PRD content]
- API Docs: [paste API documentation]
```

**Why it works:** Grounds the AI in your specific situation.

---

### 3. Task (Required)

Clear, specific instruction of what to do.

```
TASK:
Generate 10 functional test cases for the checkout flow,
covering:
- Happy path (successful purchase)
- Payment failures
- Inventory edge cases
- Session timeout scenarios
```

**Why it works:** Removes ambiguity about the expected action.

---

### 4. Constraints (Essential for QA)

Rules the AI must follow.

```
CONSTRAINTS:
- Use ONLY information from the provided PRD
- Do NOT assume features not mentioned
- If information is missing, write "Not specified"
- Do NOT invent error codes or API responses
- All test data must be realistic but fictional
```

**Why it works:** Prevents hallucinations and ensures quality.

---

### 5. Format (Highly Recommended)

Specifies output structure.

```
FORMAT:
Return test cases in this table format:
| Test ID | Description | Pre-conditions | Steps | Expected Result | Priority |
```

**Why it works:** Makes output immediately usable.

---

### 6. Examples (For Complex Tasks)

Shows what good output looks like.

```
EXAMPLE:
| TC_001 | Valid checkout | User logged in, items in cart | 
1. Click checkout 2. Enter shipping 3. Submit payment | 
Order confirmed, email sent | High |
```

**Why it works:** Demonstrates exact expectations.

---

## Complete Prompt Template

```
ROLE:
You are a [role] with expertise in [domain].

CONTEXT:
[Provide all relevant background information]
[Paste PRD, API docs, requirements]

TASK:
[Specific instruction of what to do]

CONSTRAINTS:
- [Rule 1]
- [Rule 2]
- [Rule 3]

FORMAT:
[Specify exact output structure]

EXAMPLE (optional):
[Show one complete example of expected output]
```

---

## Quick Reference: Component Priority

| Component | Priority | When to Use |
|-----------|----------|-------------|
| Task | Required | Always |
| Context | Required | Always |
| Constraints | Required | Always for QA |
| Format | High | When structure matters |
| Role | Medium | For specialized tasks |
| Examples | Medium | For complex outputs |

---

## See Also

- [What is Prompt Engineering](ch_02_what_is_prompt_engineering.md)
- [Prompt Types](ch_02_prompt_types.md)

