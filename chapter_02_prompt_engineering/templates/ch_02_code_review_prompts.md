# Code Review Prompts

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Review code from a QA perspective
**Chapter:** 2 - Prompt Engineering

---

## Template 1: General Code Review (QA Focus)

```
ROLE: You are a Senior QA Engineer reviewing code for testability.

TASK: Review this code and identify testing concerns.

REVIEW AREAS:
1. Testability issues
2. Error handling gaps
3. Edge cases not handled
4. Missing input validation
5. Potential bugs

CONSTRAINTS:
- Focus on QA-relevant issues only
- Provide specific line references
- Suggest test cases for issues found
- Do NOT rewrite the code

FORMAT:
| Line | Issue Type | Description | Suggested Test Case |

CODE:
<<<
[PASTE CODE]
>>>
```

---

## Template 2: Test Code Review

```
ROLE: You are a Test Automation Architect.

TASK: Review this test code for quality and coverage.

REVIEW AREAS:
1. Test coverage completeness
2. Assertion quality
3. Test isolation
4. Setup/teardown handling
5. Naming conventions
6. Flaky test indicators

CONSTRAINTS:
- Focus on test quality, not code style
- Identify missing test scenarios
- Flag potential flakiness

FORMAT:
| Category | Finding | Severity | Recommendation |

TEST CODE:
<<<
[PASTE TEST CODE]
>>>
```

---

## Template 3: Security Code Review

```
ROLE: You are a Security QA Specialist.

TASK: Review this code for security vulnerabilities.

SECURITY CHECKS:
- Input validation
- SQL injection risks
- XSS vulnerabilities
- Authentication/Authorization
- Sensitive data handling
- Error message exposure

CONSTRAINTS:
- Reference OWASP guidelines where applicable
- Focus on exploitable issues
- Rate severity based on impact

FORMAT:
| Line | Vulnerability | OWASP Category | Severity | Fix Recommendation |

CODE:
<<<
[PASTE CODE]
>>>
```

---

## Template 4: API Code Review

```
ROLE: You are an API QA Specialist.

TASK: Review this API endpoint code.

REVIEW AREAS:
1. Request validation
2. Response format consistency
3. Error handling
4. Status code usage
5. Authentication checks
6. Rate limiting

CONSTRAINTS:
- Check against REST best practices
- Identify missing validations
- Suggest API test cases

FORMAT:
| Issue | Description | Impact | Test Case Needed |

API CODE:
<<<
[PASTE CODE]
>>>
```

---

## Template 5: Unit Test Gap Analysis

```
ROLE: You are a QA Engineer analyzing test coverage.

TASK: Compare this code with its unit tests and identify gaps.

ANALYSIS:
1. List all functions/methods in code
2. Map existing tests to functions
3. Identify untested code paths
4. Identify missing edge case tests
5. Prioritize gaps by risk

CONSTRAINTS:
- Be specific about which paths are untested
- Suggest concrete test cases for gaps

FORMAT:
| Function | Tested Paths | Missing Paths | Priority |

SOURCE CODE:
<<<
[PASTE CODE]
>>>

TEST CODE:
<<<
[PASTE TESTS]
>>>
```

---

## Template 6: Code Complexity Review

```
ROLE: You are a QA Engineer assessing code complexity.

TASK: Review this code for complexity that impacts testing.

COMPLEXITY INDICATORS:
- Nested conditionals (high cyclomatic complexity)
- Long methods
- Multiple responsibilities
- Hidden dependencies
- Magic numbers/strings

CONSTRAINTS:
- Focus on testing impact
- Estimate test cases needed per function
- Flag maintenance risks

FORMAT:
| Function | Complexity Score | Test Cases Needed | Refactor Recommendation |

CODE:
<<<
[PASTE CODE]
>>>
```

---

## Quick Reference

| Review Type | Template |
|-------------|----------|
| General QA review | Template 1 |
| Test code quality | Template 2 |
| Security review | Template 3 |
| API endpoint | Template 4 |
| Coverage gaps | Template 5 |
| Complexity analysis | Template 6 |

---

## See Also

- [Test Case Prompts](ch_02_test_case_prompts.md)
- [Chain-of-Thought](../techniques/ch_02_chain_of_thought.md)

