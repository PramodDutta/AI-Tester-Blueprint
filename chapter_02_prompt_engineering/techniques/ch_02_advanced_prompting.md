# Advanced Prompting Techniques

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Expert-level prompting strategies for complex QA tasks
**Chapter:** 2 - Prompt Engineering

---

## Overview

Advanced prompting combines multiple techniques to solve complex problems and produce higher-quality outputs.

---

## 1. Self-Consistency Prompting

**What:** Ask the same question multiple ways and compare outputs.

**Use case:** Critical test case validation

```
Generate test cases for payment processing using three approaches:
1. First, think about happy path scenarios
2. Second, think about what can go wrong
3. Third, think about edge cases

Then consolidate into a final list, removing duplicates.
```

---

## 2. Tree of Thought (ToT)

**What:** Explore multiple reasoning paths before concluding.

**Use case:** Complex bug analysis

```
Analyze this bug using Tree of Thought:

Branch 1: Assume it's a frontend issue
- What evidence supports this?
- What tests would confirm?

Branch 2: Assume it's a backend issue
- What evidence supports this?
- What tests would confirm?

Branch 3: Assume it's a data issue
- What evidence supports this?
- What tests would confirm?

Conclusion: Which branch is most likely based on evidence?
```

---

## 3. Iterative Refinement

**What:** Build output in stages, refining each iteration.

**Use case:** Comprehensive test plans

```
PHASE 1:
List all features from the PRD.

PHASE 2:
For each feature, identify 2-3 test scenarios.

PHASE 3:
Expand each scenario into detailed test cases.

PHASE 4:
Review and add missing edge cases.
```

---

## 4. Prompt Chaining

**What:** Use output from one prompt as input for the next.

**Use case:** PRD to full test suite

```
Chain 1: Extract testable requirements from PRD
    ↓
Chain 2: Generate test scenarios for each requirement
    ↓
Chain 3: Expand scenarios into detailed test cases
    ↓
Chain 4: Add test data for each test case
```

---

## 5. Meta-Prompting

**What:** Ask the AI to improve your prompt.

**Use case:** Prompt optimization

```
I want to generate API test cases. Here's my current prompt:

"Write test cases for the login API"

How can I improve this prompt to get better, more consistent results?
Consider: specificity, constraints, format, and anti-hallucination rules.
```

---

## 6. Persona Stacking

**What:** Combine multiple expert perspectives.

**Use case:** Comprehensive review

```
Review this test plan from three perspectives:

AS A QA ENGINEER:
- Are test cases complete?
- Are edge cases covered?

AS A SECURITY EXPERT:
- Are security scenarios tested?
- Any vulnerability gaps?

AS A PERFORMANCE ENGINEER:
- Are performance scenarios included?
- Load/stress considerations?

Consolidate findings into a single review.
```

---

## 7. Constrained Generation

**What:** Strictly limit output to specific patterns.

**Use case:** Template-compliant outputs

```
Generate test cases following EXACTLY this pattern:

PATTERN:
TC_[3-digit-number] | [Functional/Negative/Boundary] | [verb] [object] [condition] | [expected outcome]

EXAMPLE:
TC_001 | Functional | Submit form with valid data | Success message displayed

Generate 5 more following this EXACT pattern. Do not deviate.
```

---

## 8. Adversarial Prompting

**What:** Ask the AI to challenge its own output.

**Use case:** Finding test gaps

```
STEP 1:
Generate 10 test cases for user registration.

STEP 2:
Now act as a critical QA reviewer. Find gaps in the test cases above:
- What scenarios are missing?
- What edge cases were overlooked?
- What could still break in production?

STEP 3:
Generate additional test cases to fill the gaps identified.
```

---

## Combining Techniques

**Example: Complete Test Suite Generation**

```
ROLE: Senior QA Engineer (Role-Based)

TASK: Generate test suite for checkout flow.

APPROACH:
1. Use Chain-of-Thought to identify all scenarios
2. Apply Self-Consistency to validate completeness
3. Use Adversarial review to find gaps
4. Apply Constrained Generation for format

CONSTRAINTS: (Anti-Hallucination)
- Use ONLY provided documentation
- Mark assumptions explicitly

OUTPUT FORMAT: (Precise Prompting)
| TC_ID | Category | Description | Steps | Expected |

DOCUMENTATION:
[Paste docs]
```

---

## Quick Reference

| Technique | Best For |
|-----------|----------|
| Self-Consistency | Validation, critical outputs |
| Tree of Thought | Bug analysis, root cause |
| Iterative Refinement | Large test plans |
| Prompt Chaining | Multi-step workflows |
| Meta-Prompting | Prompt optimization |
| Persona Stacking | Comprehensive reviews |
| Constrained Generation | Template compliance |
| Adversarial | Gap analysis |

---

## See Also

- [Chain-of-Thought](ch_02_chain_of_thought.md)
- [Role-Based Prompting](ch_02_role_based_prompting.md)
- [Precise Prompting](ch_02_precise_prompting.md)

