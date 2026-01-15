# Prompt Frameworks: STAR, CLEAR, CRISP

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Alternative frameworks for structuring prompts
**Chapter:** 2 - Prompt Engineering

---

## Framework Comparison

| Framework | Best For | Components |
|-----------|----------|------------|
| **RICE POT** | QA tasks (recommended) | Role, Intent, Context, Expected, Persona, Output, Task |
| **STAR** | Scenario-based prompts | Situation, Task, Action, Result |
| **CLEAR** | General clarity | Context, Language, Examples, Audience, Result |
| **CRISP** | Concise prompts | Context, Request, Input, Scope, Parameters |

---

## STAR Framework

**Origin:** Adapted from behavioral interview technique

```
┌─────────────────────────────────────────────────────────┐
│                    STAR FRAMEWORK                        │
├─────────────────────────────────────────────────────────┤
│  S - Situation   │  Background and context              │
│  T - Task        │  What needs to be done               │
│  A - Action      │  How to approach it                  │
│  R - Result      │  Expected outcome                    │
└─────────────────────────────────────────────────────────┘
```

### STAR Example (QA)

```
SITUATION:
We have an e-commerce checkout system that was recently updated 
with a new payment gateway. Users have reported intermittent failures.

TASK:
Create a test plan to validate the payment integration.

ACTION:
Focus on:
- Happy path transactions
- Error handling scenarios
- Timeout conditions
- Concurrent payment attempts

RESULT:
Deliver a test plan with 15-20 test cases covering all payment 
scenarios, prioritized by risk.
```

---

## CLEAR Framework

**Focus:** Ensuring clarity and avoiding ambiguity

```
┌─────────────────────────────────────────────────────────┐
│                   CLEAR FRAMEWORK                        │
├─────────────────────────────────────────────────────────┤
│  C - Context     │  Background information              │
│  L - Language    │  Tone and terminology                │
│  E - Examples    │  Sample input/output                 │
│  A - Audience    │  Who will use the output             │
│  R - Result      │  Expected deliverable                │
└─────────────────────────────────────────────────────────┘
```

### CLEAR Example (QA)

```
CONTEXT:
Testing a mobile banking app's fund transfer feature.
API documentation attached.

LANGUAGE:
Use technical QA terminology. Be precise and formal.

EXAMPLES:
Good test case: "TC_001 | Transfer $100 between accounts | 
Steps: 1. Login 2. Select transfer 3. Enter amount | 
Expected: Success message, balance updated"

AUDIENCE:
Senior QA engineers who will execute these tests.

RESULT:
10 test cases in table format covering positive and negative scenarios.
```

---

## CRISP Framework

**Focus:** Keeping prompts concise yet complete

```
┌─────────────────────────────────────────────────────────┐
│                   CRISP FRAMEWORK                        │
├─────────────────────────────────────────────────────────┤
│  C - Context     │  Essential background only           │
│  R - Request     │  Clear, specific ask                 │
│  I - Input       │  Data/documents provided             │
│  S - Scope       │  Boundaries and limitations          │
│  P - Parameters  │  Constraints and rules               │
└─────────────────────────────────────────────────────────┘
```

### CRISP Example (QA)

```
CONTEXT:
Login API endpoint needs test coverage.

REQUEST:
Generate API test cases.

INPUT:
POST /api/v1/auth/login
Body: { email, password }
Returns: 200 (token) or 401 (error)

SCOPE:
- Authentication only (not registration)
- Functional tests only (not performance)

PARAMETERS:
- Use only documented status codes
- Include positive and negative cases
- Table format output
```

---

## When to Use Which Framework

| Scenario | Recommended Framework |
|----------|----------------------|
| QA test case generation | RICE POT |
| Scenario-based analysis | STAR |
| Documentation/communication | CLEAR |
| Quick, focused prompts | CRISP |
| Complex multi-step tasks | RICE POT + Chain-of-Thought |

---

## Framework Quick Reference

```
RICE POT = Role + Intent + Context + Expected + Persona + Output + Task
STAR     = Situation + Task + Action + Result
CLEAR    = Context + Language + Examples + Audience + Result
CRISP    = Context + Request + Input + Scope + Parameters
```

---

## See Also

- [RICE POT Framework](ch_02_rice_pot_framework.md) (Recommended for QA)
- [Anatomy of a Prompt](ch_02_anatomy_of_prompt.md)

