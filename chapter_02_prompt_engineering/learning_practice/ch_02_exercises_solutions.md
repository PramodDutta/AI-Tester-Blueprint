# Chapter 2 Exercises - Solutions

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Answer Key for Prompt Engineering Exercises
**Chapter:** 2 - Prompt Engineering

---

## Exercise 1 Solution: Improve a Vague Prompt

**Improved Prompt:**
```
ROLE: You are a Senior QA Engineer.

CONTEXT: 
We are testing an e-commerce checkout application.
[Attach PRD or requirements]

TASK:
Generate 10 functional test cases for the checkout flow.

CONSTRAINTS:
- Use ONLY provided requirements
- Do NOT assume undocumented features
- Mark gaps as "Needs clarification"

FORMAT:
| Test ID | Description | Steps | Expected Result | Priority |

REQUIREMENTS:
[Paste requirements here]
```

---

## Exercise 2 Solution: Choose the Right Prompting Type

| Scenario | Answer | Why |
|----------|--------|-----|
| Generate 5 basic login test cases | Zero-Shot | Simple, standard task |
| Analyze a complex bug | Chain-of-Thought | Requires reasoning |
| Custom company template | Few-Shot | Need format examples |
| Quick validation test | Zero-Shot | Simple and direct |
| Root cause analysis | Chain-of-Thought | Multi-step reasoning |

---

## Exercise 3 Solution: Fix the Hallucination-Prone Prompt

**Fixed Prompt:**
```
ROLE: You are a QA Engineer.

TASK: Generate test cases for the payment system.

CONSTRAINTS:
- Use ONLY the provided payment documentation
- Do NOT assume payment methods not listed
- Do NOT invent error codes or messages
- Mark missing information as "[NOT SPECIFIED]"
- If unsure, state "Insufficient information"

FORMAT:
| Test ID | Category | Description | Expected Result |

PAYMENT DOCUMENTATION:
<<<
[PASTE ACTUAL DOCS HERE]
>>>
```

---

## Exercise 4 Solution: Create a Few-Shot Prompt

```
Generate API test cases following these examples:

EXAMPLE 1:
| TC_001 | DELETE /users/{id} | Valid user ID | 204 No Content | User deleted |

EXAMPLE 2:
| TC_002 | DELETE /users/{id} | Non-existent ID | 404 Not Found | Error message |

---

NOW GENERATE:
5 more DELETE endpoint test cases covering:
- Unauthorized access
- Invalid ID format
- Already deleted resource
- Missing authentication
- Rate limit exceeded
```

---

## Exercise 5 Solution: Build a Chain-of-Thought Prompt

```
TASK: Analyze test coverage for the login module.

Think through this step by step:

Step 1: List all login features from the requirements
Step 2: Map existing test cases to each feature
Step 3: Identify features without test coverage
Step 4: Identify missing edge cases and negative scenarios
Step 5: Prioritize coverage gaps by business risk

Final: Provide a coverage summary with recommendations.

REQUIREMENTS:
[Paste requirements]

EXISTING TESTS:
[Paste test list]
```

---

## Exercise 6 Solution: Role Selection

| Task | Best Role |
|------|-----------|
| Generate WCAG compliance tests | Accessibility Specialist |
| Create SQL injection test cases | Security Tester |
| Design load test scenarios | Performance Engineer |
| Review test code for flakiness | Test Automation Architect |
| Write API contract tests | API Testing Specialist |

---

## Exercise 7 Solution: Complete Prompt Construction

```
ROLE: You are a Senior QA Engineer with expertise in security testing.

CONTEXT:
Feature: Forgot Password
- User enters email
- System sends reset link  
- Link expires in 24 hours
- User creates new password
- Password must be 8+ characters

TASK:
Generate comprehensive test cases covering:
- Happy path
- Validation errors
- Security scenarios
- Edge cases

CONSTRAINTS:
- Use ONLY the PRD content above
- Do NOT assume email format validation rules (not specified)
- Do NOT assume password complexity beyond "8+ characters"
- Mark assumptions as "[ASSUMPTION]"
- If information missing, state "Not specified in PRD"

FORMAT:
| Test ID | Category | Description | Steps | Expected Result | Priority |
```

---

## Scoring Guide

| Exercise | Points | Criteria |
|----------|--------|----------|
| Exercise 1 | 15 | All 6 components included |
| Exercise 2 | 15 | Correct types with reasoning |
| Exercise 3 | 15 | Anti-hallucination constraints |
| Exercise 4 | 15 | Good examples, clear separation |
| Exercise 5 | 15 | 5 logical steps, clear flow |
| Exercise 6 | 10 | Correct role matches |
| Exercise 7 | 15 | Complete, well-structured |

**Pass:** 80+ points  
**Review:** 60-79 points  
**Retry:** Below 60 points

