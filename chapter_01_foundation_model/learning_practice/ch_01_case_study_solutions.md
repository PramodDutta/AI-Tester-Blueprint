# Chapter 1 Case Study - Solutions

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Answer Key for Applied Learning
**Chapter:** 1 - Foundation Model

---

## Case Study Solution: Screenshot + Logs → Safe Bug Report

### Correct Fact Extraction

**From Screenshot:**
| Fact | Confidence |
|------|------------|
| Error message displayed: "Invalid credentials" | Verified |
| Email field value: user@test.com | Verified |
| Password field: masked (value unknown) | Verified |
| Red error banner visible | Verified |

**From Logs:**
| Fact | Confidence |
|------|------------|
| Timestamp: 2024-01-15 10:23:45 | Verified |
| Service: AuthService | Verified |
| Endpoint: POST /api/v1/auth/login | Verified |
| Response code: 401 Unauthorized | Verified |
| Reason logged: Invalid password | Verified |

---

### Correct Missing Information List

**Critical Missing Items:**
- [ ] Expected behavior documentation (PRD)
- [ ] Is user@test.com a valid test account?
- [ ] What is the correct password for this account?
- [ ] Environment (dev/staging/prod)
- [ ] Build/version number
- [ ] Account status (active/locked/suspended)
- [ ] Previous failed login attempts

**Why These Matter:**
Without knowing the expected behavior, we cannot determine if this is:
- A bug (system should have accepted credentials)
- Expected behavior (wrong password entered)
- Test data issue (account doesn't exist)

---

### Model Safe Bug Report

```markdown
## Bug Report: Login Authentication Failure

**ID:** [To be assigned]
**Reporter:** [Name]
**Date:** 2024-01-15

### Environment
- Environment: [UNKNOWN - not provided]
- Build Version: [UNKNOWN - not provided]

### Evidence Provided
1. Screenshot of login page with error
2. Application logs from 2024-01-15 10:23:45

### Verified Facts (from evidence)

**UI Observation:**
- Login page displayed error: "Invalid credentials"
- Email entered: user@test.com

**Log Analysis:**
- Endpoint called: POST /api/v1/auth/login
- Response: 401 Unauthorized
- Log message: "Invalid password for user@test.com"

### Cannot Determine (Missing Information)
- Expected behavior for this user/password combination
- Whether correct credentials were used
- Account status in the system
- Environment and build version

### Classification
**Status:** ⚠️ PENDING CLARIFICATION

Cannot classify as bug without:
1. Confirmation that correct password was used
2. Expected behavior documentation
3. Account status verification

### Recommended Next Steps
1. Verify test account credentials
2. Check account status in database
3. Provide PRD for login behavior
```

---

### Common Mistakes to Avoid

| Mistake | Why It's Wrong | Correct Approach |
|---------|---------------|------------------|
| "Password validation is broken" | Assumes system error | State: "Login rejected, cause unknown" |
| "Database issue" | Invented root cause | State: "Root cause not determined" |
| "High priority bug" | Assumes it's a bug | State: "Pending classification" |
| "User should be able to login" | Assumes credentials are correct | State: "Cannot verify credentials" |

---

### Self-Validation Checklist (Answer Key)

| Check | Expected Answer |
|-------|-----------------|
| Are all facts from screenshot/logs? | ✅ Yes |
| Are unknowns explicitly listed? | ✅ Yes |
| Is root cause assumed? | ❌ No - marked unknown |
| Is priority assigned without evidence? | ❌ No - pending clarification |
| Can report be reproduced from evidence? | ✅ Yes |

---

## Key Learning Points

1. **Evidence First:** Only include what you can see/read
2. **Label Unknowns:** Missing info is valuable information
3. **No Assumptions:** "I don't know" is a valid answer
4. **Request Clarification:** Better than guessing wrong
5. **Reproducibility:** Report should lead to same conclusions

