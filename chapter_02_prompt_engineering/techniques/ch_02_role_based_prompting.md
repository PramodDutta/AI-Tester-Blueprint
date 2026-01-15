# Role-Based Prompting

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Assigning personas to guide AI behavior
**Chapter:** 2 - Prompt Engineering

---

## Definition

**Role-Based Prompting** assigns a specific persona, expertise level, or character to the AI, which influences how it approaches and responds to tasks.

---

## When to Use

✅ **Good for:**
- Domain-specific tasks
- Setting expertise level
- Consistent tone across outputs
- Specialized knowledge areas

❌ **Avoid when:**
- Simple factual queries
- Role adds no value
- Overcomplicating simple tasks

---

## Structure

```
ROLE: You are a [specific role] with [qualifications/experience].

[Rest of prompt...]
```

---

## QA-Specific Roles

### Role 1: Senior QA Engineer

```
ROLE: You are a Senior QA Engineer with 10+ years of experience 
in test automation, API testing, and performance testing.

TASK: Review this test plan and identify gaps.
```

**Best for:** Test case generation, coverage analysis, test planning

---

### Role 2: Security Tester

```
ROLE: You are a Security QA Specialist with expertise in 
OWASP Top 10, penetration testing, and vulnerability assessment.

TASK: Generate security test cases for this login API.
```

**Best for:** Security test cases, vulnerability analysis

---

### Role 3: Performance Engineer

```
ROLE: You are a Performance Test Engineer experienced with 
JMeter, Gatling, and load testing best practices.

TASK: Design a load test scenario for this checkout flow.
```

**Best for:** Performance test plans, load scenarios

---

### Role 4: Accessibility Tester

```
ROLE: You are an Accessibility QA Specialist with expertise 
in WCAG 2.1 guidelines and screen reader testing.

TASK: Generate accessibility test cases for this form.
```

**Best for:** WCAG compliance, a11y test cases

---

### Role 5: Critical Reviewer

```
ROLE: You are a skeptical QA Lead who questions every assumption 
and looks for edge cases others miss.

TASK: Review these test cases and find what's missing.
```

**Best for:** Gap analysis, critical review

---

## Role + Constraints (Recommended)

Combine roles with constraints for best results:

```
ROLE: You are a Senior QA Engineer with 10+ years of experience.

CONSTRAINTS:
- Use ONLY the provided PRD
- Do NOT assume undocumented features
- Mark any assumptions explicitly
- If unsure, state "Insufficient information"

TASK: Generate test cases from this PRD.
```

---

## Role Library for QA

| Role | Use Case |
|------|----------|
| Senior QA Engineer | General test case generation |
| Security Tester | Security-focused testing |
| Performance Engineer | Load/stress testing |
| Accessibility Specialist | WCAG compliance |
| Mobile QA | Mobile-specific testing |
| API Tester | API test scenarios |
| Automation Engineer | Test script review |
| QA Lead | Gap analysis, planning |

---

## Tips for Effective Roles

| Tip | Example |
|-----|---------|
| Be specific | "10+ years" not just "experienced" |
| Add domain | "in e-commerce" for context |
| Match task | Security role for security tests |
| Don't overdo | One role per prompt |

---

## Anti-Pattern: Role Overload

❌ **Bad:**
```
You are a Senior QA Engineer, Security Expert, Performance Specialist, 
and Accessibility Consultant with 20 years of experience in everything.
```

✅ **Good:**
```
You are a Senior QA Engineer with expertise in API testing.
```

---

## See Also

- [Zero-Shot Prompting](ch_02_zero_shot_prompting.md)
- [Test Case Prompts](../templates/ch_02_test_case_prompts.md)
- [Anatomy of a Prompt](../core_concepts/ch_02_anatomy_of_prompt.md)

