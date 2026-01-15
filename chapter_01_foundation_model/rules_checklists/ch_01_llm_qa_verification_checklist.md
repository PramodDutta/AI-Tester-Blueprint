# LLM QA Verification Checklist

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Manual + Automated Validation
**Audience:** QA Teams
**Chapter:** 1 - Foundation Model → QA Execution

---

## Checklist

### 1. Output Grounding
- [ ] Is the output grounded in provided input?
- [ ] Can every claim be traced back to source data?
- [ ] Are there any statements without supporting evidence?

### 2. Assumption Handling
- [ ] Are all assumptions clearly labeled?
- [ ] Are inferences marked with confidence levels?
- [ ] Are default behaviors explicitly stated (not assumed)?

### 3. Technical Accuracy
- [ ] Are versions explicitly stated?
- [ ] Are APIs correctly referenced?
- [ ] Are limits and constraints explicitly documented?
- [ ] Are error codes accurate and verifiable?

### 4. Uncertainty Management
- [ ] Is uncertainty handled correctly?
- [ ] Are "I don't know" responses used when appropriate?
- [ ] Are ambiguous areas flagged for clarification?

### 5. Consistency Check
- [ ] Is the output deterministic and repeatable?
- [ ] Are there any contradictions in the response?
- [ ] Does output align with previous verified responses?

---

## Validation Process

1. **Review** - Run through each checklist item
2. **Document** - Record findings for each section
3. **Flag** - Mark any failures or concerns
4. **Escalate** - Report unresolved issues

---

## Pass/Fail Criteria

| Status | Criteria |
|--------|----------|
| ✅ PASS | All checklist items verified |
| ⚠️ REVIEW | Minor issues, needs clarification |
| ❌ FAIL | Ungrounded claims or hallucinations detected |

