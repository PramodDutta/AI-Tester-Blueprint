# Chapter 1 Exercises

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Active Learning
**Chapter:** 1 - Foundation Model

---

## Exercise 1: Rewrite a Hallucinated Answer Safely

**Scenario:** An AI assistant produced the following response about an API:

> "The `/users` endpoint returns a maximum of 100 records per page by default. Use the `limit` parameter to adjust this. Rate limiting is set to 1000 requests per minute."

**Problem:** No API documentation was provided to the AI.

**Your Task:**
1. Identify the hallucinated claims
2. Rewrite the response following Anti-Hallucination Rules

**Safe Response Template:**
```
- Verified Facts: [None - no API documentation provided]
- Missing / Unknown Information: [List what's missing]
- Generated Output: "Insufficient information to determine."
- Self-Validation Check: [Confirm no assumptions made]
```

---

## Exercise 2: Identify Missing Inputs

**Scenario:** You're asked to write test cases for a login feature.

**Provided Input:**
- "Users should be able to log in"

**Your Task:**
1. List ALL missing information needed to write accurate test cases
2. Do NOT assume any behavior

**Missing Information Checklist:**
- [ ] Authentication method (email/username/SSO?)
- [ ] Password requirements
- [ ] Error messages for invalid credentials
- [ ] Session timeout rules
- [ ] Multi-factor authentication?
- [ ] Account lockout policy?
- [ ] API endpoints involved?
- [ ] UI elements and flow?

**Expected Output:** Request clarification, do not generate test cases.

---

## Exercise 3: Convert Vague Prompt → Safe Prompt

**Vague Prompt:**
> "Test the checkout flow"

**Your Task:** Convert this into a safe, verifiable prompt.

**Safe Prompt Template:**
```
I need to test the checkout flow.

Please provide:
1. PRD or feature specification
2. API documentation for checkout endpoints
3. Expected UI flow with screenshots
4. Valid test data (products, payment methods)
5. Error codes and expected error messages
6. Edge cases to cover

Until this information is provided, I cannot generate 
accurate test cases without risk of hallucination.
```

---

## Exercise 4: Self-Validation Practice

**Scenario:** You generated the following bug report:

> "Bug: Checkout fails with error 500 when cart has more than 10 items. 
> This is likely a database connection timeout issue."

**Your Task:** Apply the self-validation check.

| Check | Pass/Fail | Notes |
|-------|-----------|-------|
| Is "error 500" from provided logs? | | |
| Is "10 items" limit documented? | | |
| Is "database timeout" verified? | | |
| Are there unsupported assumptions? | | |

**Corrected Output:** Rewrite using only verified facts.

---

## Submission Checklist

- [ ] All exercises completed
- [ ] No invented information in responses
- [ ] All assumptions labeled
- [ ] Self-validation performed on each answer

