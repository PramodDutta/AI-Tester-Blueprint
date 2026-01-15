# Test Case Generation Prompts

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Ready-to-use prompt templates for test case generation
**Chapter:** 2 - Prompt Engineering

---

## Template 1: Basic Test Case Generation

```
ROLE: You are a Senior QA Engineer.

TASK: Generate [NUMBER] test cases for [FEATURE].

CONSTRAINTS:
- Use ONLY the provided requirements
- Do NOT assume undocumented behavior
- If information is missing, state "Not specified"

FORMAT:
| Test ID | Description | Pre-conditions | Steps | Expected Result | Priority |

REQUIREMENTS:
[PASTE REQUIREMENTS HERE]
```

---

## Template 2: PRD to Test Cases (Comprehensive)

```
ROLE: You are a Senior QA Engineer with 10+ years of experience.

TASK: Generate comprehensive test cases from this PRD.

COVERAGE AREAS:
- Functional (happy path)
- Negative scenarios
- Boundary values
- Edge cases

CONSTRAINTS:
- Use ONLY PRD content
- No assumptions about unmentioned features
- Mark unclear items as "Needs clarification"
- Do NOT invent error messages or codes

FORMAT:
| TID | Category | Description | Pre-conditions | Steps | Expected | Priority |

PRD:
<<<
[PASTE PRD HERE]
>>>
```

---

## Template 3: API Test Case Generation

```
ROLE: You are an API Testing Specialist.

TASK: Generate test cases for this API endpoint.

COVERAGE:
- Happy path (valid requests)
- Invalid inputs (validation errors)
- Authentication/Authorization
- Error handling
- Boundary conditions

CONSTRAINTS:
- Use ONLY the API documentation provided
- Include exact status codes from docs
- Do NOT assume undocumented behavior

FORMAT:
| Test ID | Endpoint | Method | Request Body | Expected Status | Expected Response |

API DOCUMENTATION:
<<<
[PASTE API DOCS HERE]
>>>
```

---

## Template 4: Negative Test Cases Only

```
ROLE: You are a QA Engineer focused on negative testing.

TASK: Generate negative test cases for [FEATURE].

FOCUS AREAS:
- Invalid inputs
- Boundary violations
- Missing required fields
- Unauthorized access
- Malformed data

CONSTRAINTS:
- Do NOT include happy path scenarios
- Each test must validate error handling
- Include expected error message if documented

FORMAT:
| Test ID | Invalid Scenario | Input | Expected Error |

FEATURE REQUIREMENTS:
[PASTE REQUIREMENTS]
```

---

## Template 5: Security Test Cases

```
ROLE: You are a Security QA Specialist.

TASK: Generate security-focused test cases for [FEATURE].

SECURITY AREAS:
- Input validation (SQL injection, XSS)
- Authentication bypass attempts
- Authorization checks
- Session management
- Data exposure

CONSTRAINTS:
- Focus on OWASP Top 10 where applicable
- Do NOT include actual malicious payloads
- Include expected secure behavior

FORMAT:
| Test ID | Security Risk | Attack Vector | Expected Secure Behavior |

FEATURE:
[PASTE FEATURE DESCRIPTION]
```

---

## Template 6: Regression Test Suite

```
ROLE: You are a QA Lead planning regression testing.

TASK: Generate a regression test suite for [MODULE].

PRIORITIES:
1. Critical business flows
2. Previously failed areas
3. High-risk integrations
4. Core functionality

CONSTRAINTS:
- Focus on end-to-end scenarios
- Include data setup requirements
- Estimate execution time per test

FORMAT:
| Test ID | Scenario | Data Setup | Steps | Est. Time | Priority |

MODULE DOCUMENTATION:
[PASTE DOCS]
```

---

## Quick Reference: Which Template to Use

| Scenario | Template |
|----------|----------|
| New feature from PRD | Template 2 |
| API endpoint testing | Template 3 |
| Error handling focus | Template 4 |
| Security audit | Template 5 |
| Release regression | Template 6 |
| Quick test cases | Template 1 |

---

## See Also

- [Bug Report Prompts](ch_02_bug_report_prompts.md)
- [API Testing Prompts](ch_02_api_testing_prompts.md)
- [Few-Shot Prompting](../techniques/ch_02_few_shot_prompting.md)

