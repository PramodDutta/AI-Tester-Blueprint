# n8n Project: Test Plan Generator

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Project Overview

Build a no-code agent that generates test plans from requirements.

---

## 📋 Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                  TEST PLAN GENERATOR                             │
└─────────────────────────────────────────────────────────────────┘

[Webhook]     [AI Agent]      [Format]       [Outputs]
    │             │              │              │
    ▼             ▼              ▼              ▼
  Receive    →  Analyze    →  Structure  →  Send to
  PRD/Story     & Generate     as Plan       Jira/Slack

```

---

## 🛠️ Step-by-Step Build

### Step 1: Create Webhook Trigger

1. Add **Webhook** node
2. Set method: POST
3. Path: `/generate-test-plan`
4. Note the webhook URL

### Step 2: Configure AI Agent

1. Add **AI Agent** node
2. Connect after Webhook
3. Configure:

**Model:** Claude 3.5 Sonnet

**System Prompt:**
```
You are a Test Plan Generator. 

Given a requirement or user story, generate:
1. Test Objectives
2. Scope (In-scope, Out-of-scope)
3. Test Approach
4. Test Cases (with priority)
5. Test Data Requirements
6. Environment Requirements
7. Risks and Mitigations

Output format: Structured markdown
```

**Input:** `{{ $json.body.requirement }}`

### Step 3: Add Output Nodes

**Option A: Slack Notification**
1. Add **Slack** node
2. Channel: #qa-team
3. Message: `{{ $json.output }}`

**Option B: Create Jira Task**
1. Add **Jira** node
2. Project: QA
3. Issue Type: Task
4. Summary: "Test Plan: [Feature Name]"
5. Description: `{{ $json.output }}`

---

## 📝 Usage

```bash
curl -X POST https://your-n8n.com/webhook/generate-test-plan \
  -H "Content-Type: application/json" \
  -d '{
    "requirement": "As a user, I want to reset my password so that I can regain access to my account if I forget my password.",
    "feature_name": "Password Reset"
  }'
```

---

## 📊 Example Output

```markdown
# Test Plan: Password Reset

## 1. Test Objectives
- Verify password reset flow works end-to-end
- Validate email delivery
- Confirm security measures

## 2. Scope
**In-scope:**
- Reset via email
- Password validation rules
- Error handling

**Out-of-scope:**
- SMS reset
- Admin password reset

## 3. Test Cases

| ID | Title | Priority |
|---|---|---|
| TC-01 | Valid email receives reset link | P0 |
| TC-02 | Invalid email shows error | P1 |
| TC-03 | Expired link is rejected | P1 |
| TC-04 | New password meets requirements | P0 |
| TC-05 | Password mismatch error | P1 |

...
```

---

## 📚 See Also

- [n8n AI Nodes](ch_05_n8n_ai_nodes.md)
- [LangFlow Setup](../langflow/ch_05_langflow_setup.md)
