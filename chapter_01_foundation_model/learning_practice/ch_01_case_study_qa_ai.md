# Chapter 1 Case Study: QA with AI

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Applied Learning
**Chapter:** 1 - Foundation Model
**Enforcement:** Anti-Hallucination Rules

---

## Case Study: Screenshot + Logs → Safe Bug Report

### Provided Input

**Screenshot Description:**
- Login page showing error message: "Invalid credentials"
- Email field contains: "user@test.com"
- Password field is masked
- Red error banner visible at top

**Log Excerpt:**
```
2024-01-15 10:23:45 [ERROR] AuthService: Authentication failed
2024-01-15 10:23:45 [DEBUG] Request: POST /api/v1/auth/login
2024-01-15 10:23:45 [DEBUG] Response: 401 Unauthorized
2024-01-15 10:23:45 [ERROR] Reason: Invalid password for user@test.com
```

---

### Step 1: Extract Verifiable Facts

| Fact | Source |
|------|--------|
| Error message: "Invalid credentials" | Screenshot |
| Email used: user@test.com | Screenshot, Logs |
| API endpoint: POST /api/v1/auth/login | Logs |
| HTTP response: 401 Unauthorized | Logs |
| Failure reason: Invalid password | Logs |
| Timestamp: 2024-01-15 10:23:45 | Logs |

---

### Step 2: List Missing / Unknown Information

- [ ] Expected behavior (is this correct system response?)
- [ ] Password requirements
- [ ] Was the correct password used?
- [ ] Is this a bug or expected validation?
- [ ] User account status (active/locked?)
- [ ] Number of failed attempts prior

---

### Step 3: Generate Safe Bug Report

**Bug Report (Safe Version):**

```
Title: Login returns 401 with "Invalid credentials" message

Environment: [MISSING - not provided]
Build Version: [MISSING - not provided]

Steps to Reproduce:
1. Navigate to login page
2. Enter email: user@test.com
3. Enter password: [masked]
4. Click login

Actual Result:
- UI displays: "Invalid credentials"
- API returns: 401 Unauthorized
- Log shows: "Invalid password for user@test.com"

Expected Result: [MISSING - PRD not provided]

Verified Evidence:
- Screenshot: Error banner visible
- Logs: Authentication failure at 2024-01-15 10:23:45

Notes:
- Cannot determine if this is a bug without expected behavior documentation
- Cannot confirm if correct password was used

Status: Needs clarification before classification as bug
```

---

### Step 4: Self-Validation Check

| Validation | Result |
|------------|--------|
| All claims traceable to input? | ✅ Yes |
| Assumptions labeled? | ✅ Yes - marked as [MISSING] |
| Invented information? | ✅ None |
| Uncertainty handled? | ✅ Yes - flagged for clarification |

---

## Anti-Pattern: Unsafe Bug Report (DO NOT DO THIS)

```
❌ UNSAFE - Contains Hallucinations:

Title: Login bug - password validation broken

The login is failing because the password validation 
service is timing out. This is probably related to the 
recent database migration. The user should be able to 
log in with these credentials.

Priority: High
Root Cause: Database connection pool exhausted
```

**Why This Is Wrong:**
- "Timing out" - not in logs
- "Database migration" - invented
- "Should be able to log in" - not verified
- "Root cause" - pure assumption

---

## Key Takeaway

> Write bug reports from evidence, not assumptions.  
> When in doubt, mark as "Unknown" and request clarification.

