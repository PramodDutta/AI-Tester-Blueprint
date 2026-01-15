# Bug Report Prompts

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Generate safe, evidence-based bug reports
**Chapter:** 2 - Prompt Engineering

---

## Template 1: Basic Bug Report from Evidence

```
ROLE: You are a QA Engineer writing a bug report.

TASK: Generate a bug report based ONLY on the evidence provided.

CONSTRAINTS:
- Use ONLY information from screenshots/logs
- Do NOT assume root cause
- Do NOT invent error codes
- Mark unknown information as "[UNKNOWN]"

FORMAT:
Title: [Brief description]
Environment: [From evidence or UNKNOWN]
Severity: [Based on impact]
Steps to Reproduce: [From evidence]
Expected Result: [From requirements or UNKNOWN]
Actual Result: [From evidence]
Evidence: [List attachments]

EVIDENCE:
<<<
[PASTE SCREENSHOT DESCRIPTION / LOGS]
>>>
```

---

## Template 2: Bug Classification

```
ROLE: You are a QA Lead classifying bugs.

TASK: Classify this bug by severity and priority.

SEVERITY DEFINITIONS:
- Critical: System crash, data loss, security breach
- High: Major feature broken, no workaround
- Medium: Feature impaired, workaround exists
- Low: Minor issue, cosmetic

CONSTRAINTS:
- Base classification ONLY on provided information
- If impact is unclear, state "Needs more information"

FORMAT:
Severity: [Level]
Priority: [Level]
Justification: [Based on evidence]
Missing Information: [What's needed]

BUG DESCRIPTION:
<<<
[PASTE BUG DESCRIPTION]
>>>
```

---

## Template 3: Bug Analysis (Chain-of-Thought)

```
ROLE: You are a Senior QA Engineer analyzing a bug.

TASK: Analyze this bug report step by step.

ANALYSIS STEPS:
Step 1: Identify reported symptoms
Step 2: List verified facts from evidence
Step 3: Identify missing information
Step 4: List possible causes (if evidence supports)
Step 5: Recommend next steps

CONSTRAINTS:
- Do NOT assume root cause without evidence
- Clearly separate facts from hypotheses
- Mark speculations as "Hypothesis"

BUG REPORT:
<<<
[PASTE BUG REPORT]
>>>
```

---

## Template 4: Bug Report Review

```
ROLE: You are a QA Lead reviewing bug reports.

TASK: Review this bug report for completeness.

CHECKLIST:
- [ ] Clear title
- [ ] Environment specified
- [ ] Steps are reproducible
- [ ] Expected vs Actual clear
- [ ] Evidence attached
- [ ] Severity justified

CONSTRAINTS:
- Identify missing information
- Suggest improvements
- Do NOT assume missing details

FORMAT:
Completeness Score: [X/6]
Missing Items: [List]
Suggested Improvements: [List]

BUG REPORT:
<<<
[PASTE BUG REPORT]
>>>
```

---

## Template 5: Convert Notes to Bug Report

```
ROLE: You are a QA Engineer writing a formal bug report.

TASK: Convert these informal notes into a proper bug report.

CONSTRAINTS:
- Use ONLY information from the notes
- Mark gaps as "[NEEDS CLARIFICATION]"
- Do NOT invent details
- Ask for missing information

FORMAT:
Title: 
Environment: 
Severity: 
Steps to Reproduce:
1.
2.
3.
Expected Result:
Actual Result:
Evidence Required:

NOTES:
<<<
[PASTE INFORMAL NOTES]
>>>
```

---

## Anti-Hallucination Reminder

```
⚠️ IMPORTANT: When generating bug reports:

✅ DO:
- Use only provided evidence
- Mark unknowns explicitly
- Request clarification for gaps

❌ DO NOT:
- Assume root cause
- Invent error messages
- Guess system behavior
- Fill gaps with assumptions
```

---

## See Also

- [Test Case Prompts](ch_02_test_case_prompts.md)
- [Chain-of-Thought](../techniques/ch_02_chain_of_thought.md)
- [Anti-Hallucination Rules](../../chapter_01_foundation_model/rules_checklists/ch_01_anti_hallucination.md)

