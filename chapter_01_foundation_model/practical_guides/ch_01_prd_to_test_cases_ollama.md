# PRD + Template → Test Case Generation using Ollama (Mistral)

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** QA-centric, production-ready guide for AI-powered test case generation
**Chapter:** 1 - Foundation Model

---

## 1. Objective (What We Are Solving)

Manual test case creation from PRDs is:

* Time-consuming
* Inconsistent across QAs
* Dependent on individual interpretation

**Goal:**
Use a **local LLM (Mistral via Ollama)** to consistently generate **high-quality, structured test cases** by feeding:

1. **PRD (Product Requirements Document)**
2. **Standardized Test Case Template**

---

## 2. Why Ollama + Mistral (QA Perspective)

### Why Local LLM?

* PRDs often contain **confidential product logic**
* No data leakage
* Faster iteration
* Cost-effective for bulk test generation

### Why Mistral?

* Strong instruction following
* Good reasoning for structured outputs
* Lightweight compared to GPT-4 class models
* Performs well for **QA-style deterministic tasks**

---

## 3. High-Level Architecture

```
PRD (Text / Markdown)
        +
Test Case Template
        ↓
Prompt Assembler
        ↓
Ollama (Mistral)
        ↓
Well-Structured Test Cases
(CSV / Table / JSON)
```

---

## 4. Inputs You Need (Very Important)

### Input 1: PRD (Cleaned)

Best practices for PRD input:

* Features
* User flows
* Validations
* Edge cases
* Non-functional hints (performance, security)

**Example (Simplified PRD):**

```
Feature: Login

Users should be able to log in using:
- Email + Password
- Google SSO

Validations:
- Email must be valid format
- Password minimum 8 characters
- Error shown for invalid credentials
- Account locked after 5 failed attempts
```

---

### Input 2: Test Case Template (Strict)

This is critical to avoid hallucinations.

**Example Template:**

```
TID
Scenario Description
Test Case ID
Pre-Condition
Steps to Execute
Expected Result
Priority
Test Type (Functional / Negative / Security)
```

---

## 5. Anti-Hallucination Rules (Mandatory)

You **must enforce these** in the prompt.

```
RULES:
- Use ONLY information from the PRD
- Do NOT assume features not mentioned
- If data is missing, write "Not Specified in PRD"
- Do NOT invent UI elements
- Generate deterministic, repeatable test cases
```

This makes the model behave like a **disciplined QA**, not a creative writer.

---

## 6. Master Prompt (Core of the System)

This is the **exact structure** you should use.

```
ROLE:
You are a Senior QA Engineer with 10+ years of experience.

TASK:
Generate high-quality test cases using the provided PRD and Test Case Template.

CONSTRAINTS:
- Use ONLY the PRD content
- Follow the template strictly
- No assumptions or hallucinations
- Clear, concise, and professional language

PRD:
<<<
{PASTE PRD HERE}
>>>

TEST CASE TEMPLATE:
<<<
{PASTE TEMPLATE HERE}
>>>

OUTPUT FORMAT:
Return test cases in tabular format suitable for CSV export.
```

---

## 7. Running It with Ollama (Command Line)

### Step 1: Pull Mistral

```bash
ollama pull mistral
```

### Step 2: Run Prompt

```bash
ollama run mistral
```

Paste the **full prompt** above and press Enter.

---

## See Also

- [PRD to Test Cases (Part 2)](ch_01_prd_to_test_cases_ollama_part2.md)
- [Anti-Hallucination Rules](../rules_checklists/ch_01_anti_hallucination.md)
- [Local LLM Setup with Ollama](ch_01_local_llm_setup_ollama.md)

