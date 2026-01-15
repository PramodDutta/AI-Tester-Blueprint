# Prompt Types

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Understanding different prompting strategies
**Chapter:** 2 - Prompt Engineering

---

## Overview

Different tasks require different prompting strategies. Choose the right type based on task complexity and available examples.

---

## The Three Main Types

```
┌─────────────────────────────────────────────────────────┐
│                    PROMPT TYPES                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ZERO-SHOT ──────→ No examples, direct instruction      │
│       ↓                                                 │
│  FEW-SHOT ───────→ 1-5 examples provided                │
│       ↓                                                 │
│  CHAIN-OF-THOUGHT → Step-by-step reasoning              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 1. Zero-Shot Prompting

**Definition:** Direct instruction without examples.

**When to use:**
- Simple, well-defined tasks
- Standard formats the model knows
- Quick iterations

**Example:**
```
Write 3 test cases for a login page with email and password fields.
Format: Test ID, Description, Steps, Expected Result
```

**Pros:** Fast, simple
**Cons:** Less control over output format

---

## 2. Few-Shot Prompting

**Definition:** Providing examples to guide the output.

**When to use:**
- Custom formats needed
- Domain-specific terminology
- Consistent style required

**Example:**
```
Generate test cases following this example:

EXAMPLE:
TC_001 | Valid Login | Enter valid email and password | User redirected to dashboard

NOW GENERATE:
3 more test cases for invalid login scenarios.
```

**Pros:** Higher consistency, better format control
**Cons:** Longer prompts, more tokens

---

## 3. Chain-of-Thought (CoT)

**Definition:** Asking the model to reason step-by-step.

**When to use:**
- Complex analysis
- Multi-step problems
- When reasoning matters

**Example:**
```
Analyze this bug report step by step:

Step 1: Identify the reported symptoms
Step 2: List possible root causes
Step 3: Determine what information is missing
Step 4: Suggest next debugging steps

Bug Report: "Checkout fails intermittently on mobile"
```

**Pros:** Better reasoning, transparent logic
**Cons:** Longer outputs, more tokens

---

## Comparison Table

| Type | Examples Needed | Best For | Token Usage |
|------|----------------|----------|-------------|
| Zero-Shot | 0 | Simple tasks | Low |
| Few-Shot | 1-5 | Custom formats | Medium |
| Chain-of-Thought | 0-2 | Complex reasoning | High |

---

## QA Use Cases by Type

| Task | Recommended Type |
|------|-----------------|
| Generate standard test cases | Zero-Shot |
| Generate test cases in custom template | Few-Shot |
| Analyze complex bug report | Chain-of-Thought |
| Write API tests | Few-Shot |
| Review test coverage | Chain-of-Thought |
| Convert requirements to tests | Few-Shot |

---

## Advanced: Combining Types

For best results, combine techniques:

```
ROLE: Senior QA Engineer

TASK: Analyze this PRD and generate test cases.

CHAIN-OF-THOUGHT:
1. First, extract all testable requirements
2. Then, identify edge cases
3. Finally, generate test cases

FEW-SHOT EXAMPLE:
| TC_001 | Requirement: User login | Steps: Enter credentials | Expected: Dashboard shown |

CONSTRAINTS:
- Use ONLY PRD content
- Mark assumptions explicitly

PRD:
[paste PRD]
```

---

## Key Takeaway

> **Match the prompt type to the task complexity.**
> - Simple → Zero-Shot
> - Custom format → Few-Shot
> - Complex reasoning → Chain-of-Thought

---

## See Also

- [Zero-Shot Prompting](../techniques/ch_02_zero_shot_prompting.md)
- [Few-Shot Prompting](../techniques/ch_02_few_shot_prompting.md)
- [Chain-of-Thought](../techniques/ch_02_chain_of_thought.md)

