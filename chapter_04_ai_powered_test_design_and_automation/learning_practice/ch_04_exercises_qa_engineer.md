# Chapter 4 Exercises - QA Engineer

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> These exercises are designed for **QA Engineers** focusing on requirement analysis, test planning, and test strategy — the core planning skills enhanced by AI.

---

## Prerequisites

- Completed [Chapter 1](../../chapter_01_foundation_model/ch_01_foundation_model.md) - Anti-hallucination rules
- Completed [Chapter 2](../../chapter_02_prompt_engineering/ch_02_prompt_engineering.md) - RICE POT framework
- Completed [Chapter 3](../../chapter_03_essential_ai_tools_setup/ch_03_essential_ai_tools_setup.md) - At least one cloud AI tool set up

---

## Exercise 1: Requirement Analysis

**Difficulty:** Beginner
**Time:** 30 minutes
**Tool:** Claude / ChatGPT (any cloud AI)

### Scenario

You are given the following Product Requirement Document (PRD) for a **Password Reset Feature**:

```
Feature: Password Reset
- User can click "Forgot Password" on login page
- User enters registered email address
- System sends reset link to email
- Reset link is valid for 24 hours
- User clicks link and enters new password
- New password must meet complexity rules
- After successful reset, user can login with new password
```

### Tasks

1. **Use RICE POT framework** to create a prompt for requirement analysis
2. **Feed the PRD to AI** and extract:
   - All testable scenarios (with IDs)
   - Ambiguities (what's unclear)
   - Gaps (what's missing)
3. **Write acceptance criteria** in GIVEN-WHEN-THEN format for each scenario
4. **Apply anti-hallucination rules** — flag any AI output that goes beyond the requirements

### Deliverables

- [ ] RICE POT prompt you used
- [ ] Extracted testable scenarios (minimum 8)
- [ ] Ambiguities identified (minimum 3)
- [ ] Gaps identified (minimum 2)
- [ ] Acceptance criteria for top 5 scenarios

---

## Exercise 2: Test Plan Generation

**Difficulty:** Intermediate
**Time:** 45 minutes
**Tool:** Claude / ChatGPT

### Scenario

You are the **QA Lead** for a new mobile banking app launch. The app has these modules:

```
Modules:
1. Account Login (Biometric + PIN)
2. View Balance & Transactions
3. Money Transfer (to registered & new recipients)
4. Bill Payment
5. Profile Settings

Constraints:
- Team: 2 QA Engineers
- Timeline: 1 sprint (2 weeks)
- Security: PCI-DSS compliance required for transfers
- Platform: iOS + Android
```

### Tasks

1. **Generate a complete test plan** using AI with RICE POT
2. **Customize the AI output** — adjust for your specific constraints
3. **Define entry and exit criteria** that are measurable
4. **Create a risk assessment** — identify top 5 risks with mitigations
5. **Define a test schedule** — break down the 2-week sprint into phases

### Deliverables

- [ ] Complete test plan document
- [ ] Risk assessment table (5 risks with severity, likelihood, mitigation)
- [ ] Test schedule with phases and daily breakdown
- [ ] Entry/exit criteria (at least 4 of each)
- [ ] Brief note: what did you change from AI output and why?

---

## Exercise 3: Test Strategy Design

**Difficulty:** Intermediate
**Time:** 40 minutes
**Tool:** Claude / ChatGPT

### Scenario

Your team recently had **2 critical bugs escape to production**:

```
Bug 1: Payment timeout not handled — users charged but orders not created
Bug 2: User data visible to other users in some edge cases (security issue)

Current state:
- Automation coverage: 40%
- Release frequency: Every 2 weeks
- Team: 3 testers
- Previous escape rate: 5% → now 12%
```

### Tasks

1. **Design a risk-based test strategy** addressing both escaped bugs
2. **Define regression priorities** — which tests MUST run every release?
3. **Recommend automation targets** — which areas to automate first?
4. **Create a shift-left action plan** — how to catch these bugs earlier
5. **Define success metrics** — how will you measure if the strategy works?

### Deliverables

- [ ] Risk-based strategy document
- [ ] Regression priority matrix (P1/P2/P3)
- [ ] Automation roadmap (what to automate, in what order)
- [ ] Shift-left actions (minimum 3 with tools)
- [ ] Success metrics with targets (e.g., "escape rate < 3%")

---

## Exercise 4: Test Case Prioritization

**Difficulty:** Advanced
**Time:** 30 minutes
**Tool:** Claude / ChatGPT

### Scenario

You have **50 test cases** but only **2 hours** to execute before release. The release includes:

```
Changes in this release:
- Bug fix: Login timeout issue
- New feature: Dark mode toggle
- Performance optimization: Search page
- Minor UI update: Button colors on homepage

Previous bugs in these areas:
- Login: 3 bugs in last 3 sprints
- Search: 1 bug last sprint
- Dark mode: New feature (untested)
- Homepage: No bugs in 6 months
```

### Tasks

1. **Use AI to prioritize** the 50 test cases based on risk
2. **Create a priority-based execution plan** for 2 hours
3. **Identify which tests to skip** and justify why
4. **Define smoke vs regression** split for this release
5. **Document your prioritization logic**

### Deliverables

- [ ] Prioritized test list (P1 → P4)
- [ ] 2-hour execution plan with time allocation
- [ ] Skipped tests with justification
- [ ] Smoke test list (must-run in first 30 min)
- [ ] Prioritization logic document

---

## Reflection Questions

After completing all exercises, answer:

1. How did RICE POT framework improve your AI prompts compared to simple questions?
2. What types of ambiguities does AI catch that you might miss manually?
3. How would you integrate AI requirement analysis into your daily QA workflow?
4. What are the limits of AI in test planning? Where do you still need human judgment?

---

## Check Solutions

→ [All Exercises Solutions](ch_04_exercises_solutions.md)
