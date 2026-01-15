# Chapter 1 Exercises - Solutions

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Answer Key for Active Learning Exercises
**Chapter:** 1 - Foundation Model

---

## Exercise 1 Solution: Rewrite a Hallucinated Answer Safely

**Original (Hallucinated):**
> "The `/users` endpoint returns a maximum of 100 records per page by default. Use the `limit` parameter to adjust this. Rate limiting is set to 1000 requests per minute."

**Identified Hallucinations:**
- "100 records per page" - Invented
- "`limit` parameter" - Invented
- "1000 requests per minute" - Invented

**Safe Response:**
```
- Verified Facts: None - no API documentation provided
- Missing / Unknown Information:
  - API documentation for /users endpoint
  - Pagination parameters and defaults
  - Rate limiting configuration
- Generated Output: "Insufficient information to determine. 
  Please provide API documentation."
- Self-Validation Check: ✅ No assumptions made
```

---

## Exercise 2 Solution: Identify Missing Inputs

**Provided:** "Users should be able to log in"

**Complete Missing Information List:**

| Category | Missing Information |
|----------|---------------------|
| Authentication | Method (email/username/phone/SSO?) |
| Authentication | Password requirements (length, complexity) |
| Authentication | MFA required? |
| Error Handling | Invalid credentials message |
| Error Handling | Account locked message |
| Error Handling | Error codes |
| Security | Lockout policy (attempts before lock) |
| Security | Session timeout duration |
| Security | Remember me functionality? |
| Technical | API endpoints |
| Technical | Request/response format |
| UI/UX | Login page elements |
| UI/UX | Success redirect location |

**Correct Action:** Do NOT generate test cases. Request:
- PRD or feature specification
- API documentation
- UI mockups/screenshots
- Error message specifications

---

## Exercise 3 Solution: Convert Vague Prompt → Safe Prompt

**Vague:** "Test the checkout flow"

**Safe Prompt:**
```
To test the checkout flow accurately, I need:

Required Documentation:
1. PRD/Feature spec for checkout
2. API documentation (endpoints, payloads, responses)
3. UI flow with screenshots or mockups

Test Data Requirements:
4. Valid product data (IDs, prices, inventory)
5. Payment methods supported
6. Shipping options and rules
7. Tax calculation rules
8. Discount/promo code behavior

Error Scenarios:
9. Error codes and messages
10. Edge cases (empty cart, out of stock, payment failure)

Without this information, I cannot generate accurate test 
cases. Please provide the above, or specify which subset 
is available.
```

---

## Exercise 4 Solution: Self-Validation Practice

**Original Bug Report:**
> "Bug: Checkout fails with error 500 when cart has more than 10 items. This is likely a database connection timeout issue."

**Self-Validation Check:**

| Check | Pass/Fail | Notes |
|-------|-----------|-------|
| Is "error 500" from provided logs? | ❌ FAIL | Not verified - need logs |
| Is "10 items" limit documented? | ❌ FAIL | Invented threshold |
| Is "database timeout" verified? | ❌ FAIL | Pure speculation |
| Are there unsupported assumptions? | ❌ FAIL | Multiple assumptions |

**Corrected Output:**
```
Title: Checkout failure reported

Verified Facts:
- [Need actual logs/screenshots to list facts]

Missing Information:
- Error logs with actual error code
- Steps that triggered the failure
- Cart contents at time of failure
- System documentation on cart limits

Generated Output:
"Insufficient information to create bug report. 
Please provide error logs and reproduction steps."

Self-Validation: ✅ No unsupported claims made
```

---

## Scoring Guide

| Exercise | Max Points | Criteria |
|----------|------------|----------|
| Exercise 1 | 25 | All hallucinations identified, safe response follows format |
| Exercise 2 | 25 | Comprehensive missing info list, no test cases generated |
| Exercise 3 | 25 | All required info categories listed, clear request format |
| Exercise 4 | 25 | All checks evaluated correctly, output rewritten safely |

**Pass:** 80+ points  
**Review:** 60-79 points  
**Retry:** Below 60 points

