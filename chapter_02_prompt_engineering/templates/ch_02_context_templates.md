# Context Creation via Templates (.md files)

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Create reusable context templates for consistent prompts
**Chapter:** 2 - Prompt Engineering

---

## Why Use Context Templates?

| Problem | Solution with Templates |
|---------|------------------------|
| Repeating same context | Write once, reuse everywhere |
| Inconsistent prompts | Standardized structure |
| Missing information | Checklist ensures completeness |
| Onboarding new team members | Ready-to-use templates |

---

## Template 1: Project Context

**File:** `context_project.md`

```markdown
# Project Context

## Application
- **Name:** [Application Name]
- **Type:** [Web / Mobile / API / Desktop]
- **Domain:** [E-commerce / Banking / Healthcare / etc.]

## Tech Stack
- **Frontend:** [React / Angular / Vue / etc.]
- **Backend:** [Node.js / Java / Python / etc.]
- **Database:** [PostgreSQL / MongoDB / etc.]
- **API Type:** [REST / GraphQL / SOAP]

## Environment
- **Dev URL:** [URL]
- **Staging URL:** [URL]
- **Prod URL:** [URL]

## Key Constraints
- [Constraint 1]
- [Constraint 2]
```

---

## Template 2: Feature Context

**File:** `context_feature.md`

```markdown
# Feature Context: [Feature Name]

## Overview
[Brief description of the feature]

## User Stories
- As a [user], I want to [action] so that [benefit]

## Acceptance Criteria
- [ ] Criteria 1
- [ ] Criteria 2
- [ ] Criteria 3

## API Endpoints (if applicable)
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST   | /api/... | ... |

## UI Elements
- [Element 1]
- [Element 2]

## Validation Rules
| Field | Rule |
|-------|------|
| Email | Valid format required |

## Error Messages
| Code | Message |
|------|---------|
| 400  | ... |
```

---

## Template 3: Test Context

**File:** `context_testing.md`

```markdown
# Testing Context

## Scope
- **In Scope:** [Features to test]
- **Out of Scope:** [Features NOT to test]

## Test Data
| Data Type | Value | Purpose |
|-----------|-------|---------|
| Valid email | test@example.com | Happy path |
| Invalid email | not-an-email | Negative test |

## Test Environment
- **Browser:** [Chrome / Firefox / Safari]
- **Device:** [Desktop / Mobile / Tablet]
- **OS:** [Windows / macOS / Linux]

## Dependencies
- [Service 1] must be running
- [Database] must have seed data

## Known Issues
- [Issue 1 - workaround]
```

---

## Template 4: Anti-Hallucination Context

**File:** `context_constraints.md`

```markdown
# Constraints & Rules

## MUST Follow
- Use ONLY information from provided documents
- Do NOT assume undocumented features
- Mark uncertainties as "[NEEDS CLARIFICATION]"
- If missing info, state "Not specified in requirements"

## MUST NOT Do
- Invent error codes or messages
- Assume validation rules not documented
- Create fictional API endpoints
- Guess system behavior

## Output Rules
- Use specified format exactly
- Include all required fields
- Mark assumptions with "[ASSUMPTION]"
```

---

## Using Templates in Prompts

### Method 1: Copy-Paste

```
CONTEXT:
[Paste content from context_project.md]
[Paste content from context_feature.md]

TASK:
Generate test cases...
```

### Method 2: Reference Files

```
CONTEXT:
See attached files:
- context_project.md
- context_feature.md
- context_constraints.md

TASK:
Using the context from the attached files, generate...
```

---

## Folder Structure

```
📁 prompts/
├── 📁 context/
│   ├── context_project.md
│   ├── context_constraints.md
│   └── 📁 features/
│       ├── context_login.md
│       ├── context_checkout.md
│       └── context_payment.md
├── 📁 templates/
│   ├── template_test_cases.md
│   ├── template_bug_report.md
│   └── template_api_tests.md
└── README.md
```

---

## Quick Start: Create Your First Template

1. Create `context_project.md` with your app details
2. Create `context_constraints.md` with anti-hallucination rules
3. Create feature-specific context files as needed
4. Reference templates in your prompts

---

## See Also

- [RICE POT Framework](../core_concepts/ch_02_rice_pot_framework.md)
- [Test Case Prompts](ch_02_test_case_prompts.md)
- [Steps for Effective Prompting](../core_concepts/ch_02_steps_effective_prompting.md)

