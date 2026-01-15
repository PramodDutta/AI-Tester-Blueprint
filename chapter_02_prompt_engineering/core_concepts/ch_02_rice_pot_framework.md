# RICE POT Framework

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** A structured approach to crafting effective prompts
**Chapter:** 2 - Prompt Engineering

---

## Overview

**RICE POT** is a memorable framework for building complete, effective prompts. It ensures you include all critical components for consistent, high-quality AI outputs.

```
┌─────────────────────────────────────────────────────────┐
│                    RICE POT FRAMEWORK                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   R - Role           │   P - Persona / Parameters       │
│   I - Intent         │   O - Output Format              │
│   C - Context        │   T - Task                       │
│   E - Expected Output│                                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## RICE - The Foundation

### R - Role (Expertise)

**What:** The professional identity and expertise level of the AI.

**Purpose:** Sets the knowledge domain and skill level.

```
ROLE: You are a Senior QA Engineer with 10+ years of experience 
in test automation and API testing.
```

**Examples:**
- "You are a Security Testing Specialist"
- "You are a Performance Engineer"
- "You are an Accessibility QA Expert"

---

### I - Intent (Why)

**What:** The purpose behind the request.

**Purpose:** Helps AI understand the goal, not just the task.

```
INTENT: I need to ensure complete test coverage before release 
to prevent production bugs.
```

**Examples:**
- "I need to validate API changes don't break existing integrations"
- "I want to identify security vulnerabilities before deployment"
- "I need to document test cases for audit compliance"

---

### C - Context (Background)

**What:** All relevant background information.

**Purpose:** Grounds the AI in your specific situation.

```
CONTEXT:
- Application: E-commerce checkout system
- Tech stack: React + Node.js
- Recent changes: Payment gateway integration
- PRD: [attached]
```

**Include:**
- PRD / Requirements
- API documentation
- Screenshots / Logs
- System constraints
- Previous issues

---

### E - Expected Output (Success Criteria)

**What:** What successful output looks like.

**Purpose:** Defines the quality bar and acceptance criteria.

```
EXPECTED OUTPUT:
- 10 test cases minimum
- Cover happy path and error scenarios
- Include boundary value tests
- Each test must be independently executable
```

---

## POT - The Refinement

### P - Persona / Parameters

**What:** Behavioral style OR constraints and rules.

**Purpose:** Controls HOW the AI approaches the task.

#### Option A: Persona (Behavior)

```
PERSONA: Be skeptical and thorough. Question every assumption.
Look for edge cases others might miss. Never accept requirements 
at face value.
```

#### Option B: Parameters (Constraints)

```
PARAMETERS:
- Use ONLY provided documentation
- Do NOT assume undocumented features
- Mark uncertainties as "[NEEDS CLARIFICATION]"
- No hallucinations allowed
```

**Recommendation:** Use Parameters for QA tasks to prevent hallucinations.

---

### O - Output Format

**What:** The exact structure of the response.

**Purpose:** Makes output immediately usable.

```
OUTPUT FORMAT:
| Test ID | Category | Description | Steps | Expected Result | Priority |
```

**Formats:**
- Table / CSV
- JSON
- Bullet list
- Numbered steps
- Custom template

---

### T - Task (What to Do)

**What:** The specific action to perform.

**Purpose:** Clear, unambiguous instruction.

```
TASK: Generate 10 functional test cases for the checkout flow,
covering:
1. Happy path (successful purchase)
2. Payment failures
3. Cart edge cases
4. Session timeout
```

---

## Complete RICE POT Template

```
=== RICE ===

ROLE:
You are a [job title] with expertise in [domain].

INTENT:
I need to [goal/purpose] because [reason].

CONTEXT:
- Application: [name]
- Documentation: [attached below]
- Constraints: [any limitations]

EXPECTED OUTPUT:
- [Success criteria 1]
- [Success criteria 2]
- [Quality bar]

=== POT ===

PARAMETERS:
- Use ONLY provided information
- Do NOT assume undocumented features
- Mark gaps as "[NOT SPECIFIED]"

OUTPUT FORMAT:
[Specify exact format - table, JSON, list, etc.]

TASK:
[Specific instruction of what to do]

=== INPUT ===

[Paste PRD / API docs / Requirements here]
```

---

## Quick Reference Card

| Component | Question It Answers | Example |
|-----------|---------------------|---------|
| **R**ole | Who are you? | Senior QA Engineer |
| **I**ntent | Why do this? | Ensure release quality |
| **C**ontext | What's the situation? | PRD, API docs, constraints |
| **E**xpected | What's success? | 10 test cases, no gaps |
| **P**arameters | What are the rules? | No assumptions, cite sources |
| **O**utput | What format? | Table with 5 columns |
| **T**ask | What exactly to do? | Generate test cases |

---

## See Also

- [Anatomy of a Prompt](ch_02_anatomy_of_prompt.md)
- [Anti-Hallucination Rules](../../chapter_01_foundation_model/rules_checklists/ch_01_anti_hallucination.md)
- [Test Case Prompts](../templates/ch_02_test_case_prompts.md)

