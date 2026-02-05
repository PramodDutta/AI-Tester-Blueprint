# Chapter 4 Exercises - SDET

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> These exercises are designed for **SDETs (Software Development Engineers in Test)** focusing on test design techniques, bug reporting, and metrics analysis — the bridge between QA process and technical implementation.

---

## Prerequisites

- Completed [Chapter 1](../../chapter_01_foundation_model/ch_01_foundation_model.md) - Foundation
- Completed [Chapter 2](../../chapter_02_prompt_engineering/ch_02_prompt_engineering.md) - RICE POT
- Completed [Chapter 3](../../chapter_03_essential_ai_tools_setup/ch_03_essential_ai_tools_setup.md) - Tools set up
- Basic understanding of testing frameworks (pytest, Playwright)

---

## Exercise 1: AI-Powered Test Design Techniques

**Difficulty:** Intermediate
**Time:** 45 minutes
**Tool:** Claude / ChatGPT + VS Code

### Scenario

Design a comprehensive test suite for a **Coupon Code System** using AI-assisted techniques:

```
Business Rules:
- Coupon codes: WELCOME10, SUMMER20, FLASH50
- WELCOME10: 10% off, one-time use per account, valid 30 days
- SUMMER20: 20% off, unlimited uses, valid June 1 - Aug 31 only
- FLASH50: 50% off, first 100 users only, valid 24 hours
- Minimum order: $25 for any coupon
- Coupons cannot be combined
- Discount applies to subtotal only (before tax/shipping)
```

### Tasks

1. **Equivalence Partitioning** — Use AI to identify all equivalence classes for coupon validation
2. **Decision Table** — Create a decision table for all coupon + user + order combinations
3. **Boundary Value Analysis** — Identify boundaries for order amounts, usage limits, validity dates
4. **State Transitions** — Map coupon states (Active, Expired, Used Up, Invalid)
5. **Error Guessing** — Predict top 5 likely bugs based on the business rules

### Deliverables

- [ ] Equivalence partition table (minimum 12 classes)
- [ ] Decision table (cover all rule combinations)
- [ ] Boundary values (minimum 10 test values)
- [ ] State transition diagram with 8+ transitions
- [ ] Error guessing test cases (5 predicted bugs with test cases)
- [ ] Total test count: How many unique tests from all techniques?

---

## Exercise 2: Bug Report Generation & Classification

**Difficulty:** Intermediate
**Time:** 35 minutes
**Tool:** Claude / ChatGPT + Jira knowledge

### Scenario

You found the following bugs during testing. Convert each into a proper bug report:

**Bug Observation 1:**
```
"The coupon FLASH50 applies even after 100 users have used it.
I'm user #105 and it still worked."
```

**Bug Observation 2:**
```
"When I apply SUMMER20 coupon and then change the cart to below
$25, the discount stays applied."
```

**Bug Observation 3:**
```
"Page takes 15 seconds to load after applying coupon on mobile Chrome."
```

### Tasks

1. **Convert each observation** into a complete bug report using AI
2. **Classify severity** for each bug with justification
3. **Write reproduction steps** that are clear and numbered
4. **Add root cause hypotheses** for each bug
5. **Define acceptance criteria for fix verification** for each bug
6. **Format for Jira** — ready to copy-paste

### Deliverables

- [ ] 3 complete bug reports (Jira format)
- [ ] Severity classification with justification for each
- [ ] Root cause hypothesis for each (minimum 2 per bug)
- [ ] Fix verification steps for each (minimum 3 steps)
- [ ] Priority assignment with business impact explanation

---

## Exercise 3: Test Metrics Dashboard

**Difficulty:** Advanced
**Time:** 50 minutes
**Tool:** Python + Claude / ChatGPT

### Scenario

You have the following test data from 3 sprints. Create a metrics dashboard and generate insights:

```python
sprint_data = {
    "Sprint 10": {
        "total_tests": 180,
        "passed": 145,
        "failed": 25,
        "skipped": 10,
        "bugs_found": 12,
        "bugs_fixed": 10,
        "bugs_escaped": 1,
        "automation_count": 90,
        "execution_time_minutes": 120
    },
    "Sprint 11": {
        "total_tests": 210,
        "passed": 185,
        "failed": 18,
        "skipped": 7,
        "bugs_found": 15,
        "bugs_fixed": 13,
        "bugs_escaped": 2,
        "automation_count": 115,
        "execution_time_minutes": 95
    },
    "Sprint 12": {
        "total_tests": 250,
        "passed": 210,
        "failed": 28,
        "skipped": 12,
        "bugs_found": 18,
        "bugs_fixed": 15,
        "bugs_escaped": 2,
        "automation_count": 162,
        "execution_time_minutes": 80
    }
}
```

### Tasks

1. **Calculate key metrics** for each sprint (pass rate, automation ratio, escape rate)
2. **Identify trends** — what's improving? What's concerning?
3. **Use AI to generate insights** — what do the numbers say?
4. **Create a Python dashboard script** that prints formatted metrics
5. **Generate a sprint summary report** using AI (executive-friendly)
6. **Define next sprint targets** based on the data

### Deliverables

- [ ] Metrics calculation table (all sprints side by side)
- [ ] Trend analysis (minimum 5 observations)
- [ ] Python dashboard script (runnable)
- [ ] Sprint summary report (3 paragraphs: summary, risks, recommendations)
- [ ] Next sprint targets with specific numbers

---

## Exercise 4: Combined SDET Walkthrough

**Difficulty:** Advanced
**Time:** 60 minutes
**Tool:** All tools (AI + VS Code + Python)

### Scenario

End-to-end exercise: Take a feature through the complete SDET lifecycle.

```
Feature: Search with Filters
- Search bar on product listing page
- Filters: Category, Price Range, Brand, Rating
- Sort options: Price (Low-High), Price (High-Low), Rating, Relevance
- Results show product name, price, rating, image
- "No results" message when nothing matches
- Search is case-insensitive
```

### Tasks

1. **Design tests** using equivalence partitioning + error guessing
2. **Write a bug report** for a realistic bug you identify in the requirements
3. **Calculate test metrics** — how many tests, what coverage?
4. **Generate a test execution plan** with priorities
5. **Create metrics projections** — predict sprint metrics if all tests pass

### Deliverables

- [ ] Test design document (all techniques applied)
- [ ] At least 1 bug report from requirement analysis
- [ ] Metrics plan (targets and projections)
- [ ] Prioritized test execution plan
- [ ] Full walkthrough document showing your process

---

## Reflection Questions

1. How did decision tables help catch edge cases you wouldn't have thought of manually?
2. What made the bug reports more effective when AI was involved vs. writing them manually?
3. What metrics surprised you most when analyzing the sprint data trends?
4. As an SDET, how would you integrate these techniques into your daily workflow?

---

## Check Solutions

→ [All Exercises Solutions](ch_04_exercises_solutions.md)
