# Chapter 2 Exercises

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Active Learning for Prompt Engineering
**Chapter:** 2 - Prompt Engineering

---

## Exercise 1: Improve a Vague Prompt

**Vague Prompt:**
```
Write some tests for the app.
```

**Your Task:**
Transform this into an effective prompt using the 6 components:
1. Role
2. Context
3. Task
4. Constraints
5. Format
6. Examples (optional)

**Write your improved prompt below:**

```
[YOUR ANSWER HERE]
```

---

## Exercise 2: Choose the Right Prompting Type

For each scenario, identify the best prompting type (Zero-Shot, Few-Shot, or Chain-of-Thought):

| Scenario | Your Answer | Why? |
|----------|-------------|------|
| Generate 5 basic login test cases | | |
| Analyze a complex bug with multiple symptoms | | |
| Generate test cases in custom company template | | |
| Quick validation of input field | | |
| Root cause analysis of intermittent failure | | |

---

## Exercise 3: Fix the Hallucination-Prone Prompt

**Original Prompt (Prone to Hallucinations):**
```
Generate test cases for the payment system.
Include all edge cases and error scenarios.
```

**Problems:**
- No constraints
- No context
- Open to assumptions

**Your Task:**
Rewrite with anti-hallucination safeguards.

**Fixed Prompt:**
```
[YOUR ANSWER HERE]
```

---

## Exercise 4: Create a Few-Shot Prompt

**Task:** Generate API test cases for a DELETE endpoint.

**Your Task:**
1. Write 2 example test cases
2. Add proper separation
3. Write the instruction for generating more

**Your Few-Shot Prompt:**
```
[YOUR ANSWER HERE]
```

---

## Exercise 5: Build a Chain-of-Thought Prompt

**Scenario:** You need to analyze test coverage for a login module.

**Your Task:**
Create a CoT prompt with 5 clear steps.

**Your CoT Prompt:**
```
[YOUR ANSWER HERE]
```

---

## Exercise 6: Role Selection

Match the best role for each QA task:

| Task | Best Role |
|------|-----------|
| Generate WCAG compliance tests | |
| Create SQL injection test cases | |
| Design load test scenarios | |
| Review test code for flakiness | |
| Write API contract tests | |

**Available Roles:**
- Senior QA Engineer
- Security Tester
- Performance Engineer
- Accessibility Specialist
- Test Automation Architect
- API Testing Specialist

---

## Exercise 7: Complete Prompt Construction

**Scenario:** You need to generate test cases from a PRD for a new "forgot password" feature.

**Provided PRD:**
```
Feature: Forgot Password
- User enters email
- System sends reset link
- Link expires in 24 hours
- User creates new password
- Password must be 8+ characters
```

**Your Task:**
Write a complete prompt with:
- Role
- Context (use the PRD above)
- Task
- Constraints (anti-hallucination)
- Format (table)

**Your Complete Prompt:**
```
[YOUR ANSWER HERE]
```

---

## Submission Checklist

- [ ] All 7 exercises completed
- [ ] Prompts include constraints
- [ ] Anti-hallucination rules applied
- [ ] Formats specified where needed
- [ ] Appropriate prompting type used

---

## See Also

- [Exercises Solutions](ch_02_exercises_solutions.md)
- [Anatomy of a Prompt](../core_concepts/ch_02_anatomy_of_prompt.md)

