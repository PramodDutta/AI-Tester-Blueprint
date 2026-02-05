# Chapter 4 Exercises - Solutions

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> Reference solutions for all Chapter 4 exercises across QA Engineer, SDET, and Automation Tester roles.

---

## QA Engineer Solutions

### Exercise 1: Requirement Analysis — Solution

**RICE POT Prompt Used:**
```text
Role: Senior QA Engineer with 10+ years in requirement analysis
Intent: Analyze password reset requirements and extract testable scenarios
Context: [Password Reset PRD as given]
Expected Output: Scenarios, ambiguities, gaps, acceptance criteria
Parameters: Include positive, negative, edge cases. Flag assumptions.
Output Format: Structured tables
Task: Perform complete analysis.
```

**Testable Scenarios (10):**

| ID | Scenario | Type | Priority |
|----|----------|------|----------|
| SC-001 | Reset with valid registered email | Positive | Critical |
| SC-002 | Reset with unregistered email | Negative | High |
| SC-003 | Reset with invalid email format | Negative | High |
| SC-004 | Click valid reset link within 24 hours | Positive | Critical |
| SC-005 | Click expired reset link (> 24 hours) | Negative | Critical |
| SC-006 | Enter new password meeting complexity | Positive | Critical |
| SC-007 | Enter new password NOT meeting complexity | Negative | High |
| SC-008 | Login with new password after reset | Positive | Critical |
| SC-009 | Request multiple reset links | Edge | Medium |
| SC-010 | Use reset link twice (replay attack) | Edge | High |

**Ambiguities (3+):**
1. What happens if user requests reset but never uses it?
2. Can user request another reset while first link is still valid?
3. Does reset link invalidate after use?
4. Rate limiting on reset requests?

**Gaps (2+):**
1. No mention of what happens to active sessions after password reset
2. No specification for reset link format or security requirements
3. No mention of audit logging for reset events

**Sample Acceptance Criteria:**
```
AC-001:
GIVEN a registered user
WHEN they enter their email and click "Reset Password"
THEN a reset link is sent to their email within 30 seconds

AC-002:
GIVEN a reset link was generated more than 24 hours ago
WHEN user clicks the reset link
THEN error message "Reset link has expired" is displayed
```

---

### Exercise 2: Test Plan Generation — Solution

**Key sections of the expected test plan:**

```
RISK ASSESSMENT (Top 5):
| Risk | Severity | Likelihood | Mitigation |
| Payment failure in transfers | Critical | High | Sandbox testing + dual verification |
| Biometric auth failure | Critical | Medium | Fallback to PIN |
| Data breach (PCI-DSS) | Critical | Low | Penetration testing + compliance scan |
| iOS/Android inconsistency | High | High | Device matrix testing |
| Performance on low-end devices | High | Medium | Load testing on target devices |

TEST SCHEDULE (2 weeks):
- Days 1-2: Test planning, environment setup
- Days 3-5: Test case design + automation script creation
- Days 6-8: Functional execution (manual + automated)
- Days 9-10: Bug fix verification
- Days 11-12: Regression + performance
- Days 13-14: Final sign-off + report
```

---

### Exercise 3: Test Strategy — Solution

**Key strategy elements:**

```
PRIORITY ACTIONS (based on 2 escaped bugs):

1. Payment timeout: Add specific regression tests
   - Timeout simulation test
   - Idempotency key verification
   - Retry logic validation
   Automation: 100%

2. Data isolation: Add security regression
   - Cross-user data access tests
   - Session isolation verification
   Automation: 80% + manual security probes

3. Shift-left additions:
   - Contract tests for payment API
   - Security scan in CI/CD
   - Code review checklist for data access patterns

SUCCESS METRICS:
- Escape rate target: < 3% (from 12%)
- Regression suite: runs every deployment
- Automation coverage: 60% (from 40%) within 2 sprints
```

---

### Exercise 4: Prioritization — Solution

```
PRIORITIZATION LOGIC:
P1 (Must Run — Smoke): Login + core navigation (5 tests, 15 min)
P2 (Must Run — Bug Fix): Login timeout regression (3 tests, 10 min)
P3 (Should Run — New Feature): Dark mode (8 tests, 25 min)
P4 (Run If Time): Homepage UI, search performance (remaining)

SKIP JUSTIFICATION:
- Homepage visual tests: No changes, no bugs in 6 months
- Non-critical filter tests: Not in release scope
- Keep: All login + search tests (recent bugs)

2-HOUR PLAN:
- 0:00-0:15  → Smoke (5 critical tests)
- 0:15-0:25  → Login regression (3 bug-fix tests)
- 0:25-0:50  → Dark mode (8 new feature tests)
- 0:50-1:10  → Search performance
- 1:10-1:40  → Login edge cases
- 1:40-2:00  → Buffer / re-run failures
```

---

## SDET Solutions

### Exercise 1: Test Design Techniques — Solution

**Equivalence Partitions (12):**

| EP-ID | Class | Representative | Expected |
|-------|-------|----------------|----------|
| EP-01 | Valid coupon, valid order | WELCOME10, $50 order | 10% off |
| EP-02 | Expired coupon | SUMMER20 in September | "Coupon expired" |
| EP-03 | Invalid coupon code | "FAKE99" | "Invalid coupon" |
| EP-04 | Order below minimum | WELCOME10, $20 order | "Minimum $25 required" |
| EP-05 | Already-used coupon (one-time) | WELCOME10, used | "Already used" |
| EP-06 | FLASH50 after 100 uses | User #101 | "Coupon unavailable" |
| EP-07 | Empty coupon field | "" | "Enter coupon code" |
| EP-08 | Coupon before valid date | SUMMER20 in May | "Not yet valid" |
| EP-09 | Case sensitivity | "welcome10" vs "WELCOME10" | Depends on implementation |
| EP-10 | Multiple coupons at once | WELCOME10 + SUMMER20 | "Only one coupon allowed" |
| EP-11 | Valid coupon, exact minimum | WELCOME10, $25.00 | 10% off |
| EP-12 | Whitespace in coupon | " WELCOME10 " | Should trim and validate |

**Decision Table (partial):**

| Rule | Coupon | Valid? | Order >= $25 | Not Used | Discount |
|------|--------|--------|--------------|----------|----------|
| R1 | WELCOME10 | Yes | Yes | Yes | 10% |
| R2 | WELCOME10 | Yes | Yes | No | "Already used" |
| R3 | WELCOME10 | Yes | No | Yes | "Min $25" |
| R4 | SUMMER20 | Yes | Yes | - | 20% |
| R5 | FLASH50 | Yes, <100 | Yes | - | 50% |
| R6 | FLASH50 | Yes, >100 | Yes | - | "Unavailable" |
| R7 | Any | No | Any | Any | "Invalid" |

**Error Guessing (top 5 predicted bugs):**
1. FLASH50 counter not atomic — race condition allows >100 uses
2. WELCOME10 "one-time" check bypassed by clearing browser cache
3. SUMMER20 date validation uses server timezone, not user timezone
4. Coupon discount calculated on tax-included price, not subtotal
5. Changing cart after coupon applied doesn't re-validate minimum

---

### Exercise 2: Bug Reports — Solution

**Bug 1 — FLASH50 limit not enforced:**
```
Severity: Critical (financial impact — giving away 50% discount)
Priority: P1
Root Cause Hypothesis:
  1. Counter is not atomic (race condition in DB)
  2. Counter checked but not decremented in same transaction
  3. Cached counter value used instead of real-time DB query
```

**Bug 2 — Minimum order validation not re-checked:**
```
Severity: High (discount applied incorrectly)
Priority: P2
Root Cause Hypothesis:
  1. Validation only runs on coupon apply, not on cart change
  2. Frontend removes validation after initial apply
  3. Backend doesn't re-validate on checkout
```

**Bug 3 — Slow page on mobile after coupon:**
```
Severity: Medium (performance, not data loss)
Priority: P3
Root Cause Hypothesis:
  1. Coupon validation API call blocking page render
  2. Mobile-specific rendering issue after DOM update
  3. Large payload in coupon response not optimized for mobile
```

---

### Exercise 3: Metrics Dashboard — Solution

**Calculated Metrics:**

| Metric | Sprint 10 | Sprint 11 | Sprint 12 | Trend |
|--------|-----------|-----------|-----------|-------|
| Pass Rate | 80.6% | 88.1% | 84.0% | ↕ Fluctuating |
| Automation Ratio | 50.0% | 54.8% | 64.8% | ↑ Growing |
| Escape Rate | 8.3% | 13.3% | 11.1% | ⚠️ High |
| Fix Rate | 83.3% | 86.7% | 83.3% | → Stable |
| Exec Time | 120 min | 95 min | 80 min | ↓ Improving |

**Python Dashboard Script:**
```python
#!/usr/bin/env python3
"""SDET Exercise 3 - Metrics Dashboard Solution."""

sprint_data = {
    "Sprint 10": {"total": 180, "passed": 145, "failed": 25, "skipped": 10,
                  "bugs_found": 12, "bugs_fixed": 10, "escaped": 1, "auto": 90, "time": 120},
    "Sprint 11": {"total": 210, "passed": 185, "failed": 18, "skipped": 7,
                  "bugs_found": 15, "bugs_fixed": 13, "escaped": 2, "auto": 115, "time": 95},
    "Sprint 12": {"total": 250, "passed": 210, "failed": 28, "skipped": 12,
                  "bugs_found": 18, "bugs_fixed": 15, "escaped": 2, "auto": 162, "time": 80},
}

def calculate_metrics(data):
    return {
        "pass_rate": (data["passed"] / data["total"]) * 100,
        "auto_ratio": (data["auto"] / data["total"]) * 100,
        "escape_rate": (data["escaped"] / data["bugs_found"]) * 100 if data["bugs_found"] > 0 else 0,
        "fix_rate": (data["bugs_fixed"] / data["bugs_found"]) * 100 if data["bugs_found"] > 0 else 0,
    }

# Generate dashboard
print("=" * 60)
print(f"{'SPRINT METRICS COMPARISON':^60}")
print("=" * 60)
print(f"{'Metric':<20} {'Sprint 10':>12} {'Sprint 11':>12} {'Sprint 12':>12}")
print("-" * 60)

for sprint, data in sprint_data.items():
    m = calculate_metrics(data)
    if sprint == "Sprint 10":
        print(f"{'Pass Rate':<20} {m['pass_rate']:>11.1f}%", end="")
    elif sprint == "Sprint 11":
        print(f" {calculate_metrics(sprint_data['Sprint 11'])['pass_rate']:>11.1f}%", end="")
    else:
        print(f" {calculate_metrics(sprint_data['Sprint 12'])['pass_rate']:>11.1f}%")

# Output more rows...
```

**Dashboard Output:**
```
============================================================
              SPRINT METRICS COMPARISON
============================================================
Metric               Sprint 10    Sprint 11    Sprint 12
------------------------------------------------------------
Pass Rate               80.6%        88.1%        84.0%
Automation Ratio        50.0%        54.8%        64.8%
Escape Rate              8.3%        13.3%        11.1%  ⚠️
Fix Rate                83.3%        86.7%        83.3%
Exec Time (min)           120           95           80  ↓
============================================================

⚠️ ALERTS:
  - Escape rate > 10% in Sprint 11 & 12 — investigate root cause
  - Failed test count increased: 25 → 28 (+3)

✅ WINS:
  - Automation ratio grew +14.8 points over 3 sprints
  - Execution time reduced by 33% (120 → 80 min)

🎯 SPRINT 13 TARGETS:
  - Escape rate: < 5%
  - Automation ratio: 70%
  - Pass rate: > 90%
```

**Key Insights:**
1. Automation growing (+15% in 3 sprints) — driving faster execution
2. Escape rate concerning — above 10% in last 2 sprints
3. Execution time dropping — automation paying off
4. Failed tests increasing (25→28) despite more tests — new features have issues
5. Skip rate increasing (10→12) — investigate blocked tests

---

## Automation Tester Solutions

### Exercise 1: Playwright Code — Solution

**Page Object:**
```python
class LoginPage(BasePage):
    def __init__(self, page: Page):
        super().__init__(page)
        self.email = page.locator('#email')
        self.password = page.locator('#password')
        self.remember_me = page.locator('#remember-me')
        self.submit = page.locator('.login-btn')
        self.error_msg = page.locator('.error-msg')
        self.forgot_pwd = page.locator('#forgot-pwd')

    async def login(self, email: str, password: str, remember: bool = False):
        await self.navigate("/login")
        await self.email.fill(email)
        await self.password.fill(password)
        if remember:
            await self.remember_me.check()
        await self.submit.click()
```

**Key test patterns:**
```python
# Parametrized validation tests
@pytest.mark.parametrize("email,password,expected_error", [
    ("", "Pass@123", "Email is required"),
    ("user@test.com", "", "Password is required"),
    ("invalid", "Pass@123", "Invalid email format"),
])
async def test_login_validation(page, email, password, expected_error):
    login = LoginPage(page)
    await login.login(email, password)
    error = await login.get_error()
    assert error == expected_error
```

**Code review notes:**
- Verify `#email`, `#password` IDs match actual DOM
- Copilot may suggest `time.sleep()` — replace with Playwright waits
- Add `await expect(element).to_be_visible()` before interactions

---

### Exercise 2: Claude Code Walkthrough — Solution

**Phase 1: Project Setup Command**
```bash
mkdir cart-test && cd cart-test
claude
```

**Phase 2: Setup Prompt & Output**
```
You: Set up a Playwright Python project with Page Object Model for shopping cart testing

Claude Code creates:
cart-test/
├── tests/
│   ├── pages/
│   │   ├── __init__.py
│   │   ├── base_page.py
│   │   ├── product_page.py
│   │   └── cart_page.py
│   ├── e2e/
│   │   ├── __init__.py
│   │   └── test_cart.py
│   └── conftest.py
├── requirements.txt
└── pytest.ini
```

**Phase 3: Generated CartPage.py**
```python
# tests/pages/cart_page.py
from playwright.sync_api import Page, expect

class CartPage:
    def __init__(self, page: Page):
        self.page = page
        self.cart_items = page.locator('.cart-item')
        self.qty_inputs = page.locator('.qty-input')
        self.remove_buttons = page.locator('.remove-btn')
        self.cart_total = page.locator('.cart-total')
        self.empty_message = page.locator('.empty-cart-message')
        self.checkout_button = page.locator('.checkout-btn')

    def navigate(self):
        self.page.goto('/cart')

    def get_item_count(self) -> int:
        return self.cart_items.count()

    def update_quantity(self, item_index: int, quantity: int):
        self.qty_inputs.nth(item_index).fill(str(quantity))
        self.page.wait_for_load_state('networkidle')

    def remove_item(self, item_index: int):
        self.remove_buttons.nth(item_index).click()

    def get_total(self) -> str:
        return self.cart_total.inner_text()

    def is_empty(self) -> bool:
        return self.empty_message.is_visible()

    def checkout(self):
        expect(self.checkout_button).to_be_visible()
        self.checkout_button.click()
```

**Phase 4: Generated Test File**
```python
# tests/e2e/test_cart.py
import pytest
from playwright.sync_api import Page, expect
from tests.pages.cart_page import CartPage
from tests.pages.product_page import ProductPage

def test_add_item_to_cart(page: Page):
    """Add single item and verify it appears in cart."""
    product = ProductPage(page)
    product.navigate_to_product(101)
    product.add_to_cart()

    cart = CartPage(page)
    cart.navigate()
    assert cart.get_item_count() == 1

def test_cart_total_updates(page: Page, cart_with_item):
    """Verify total updates when quantity changes."""
    cart = CartPage(cart_with_item)
    initial_total = cart.get_total()
    cart.update_quantity(0, 3)
    assert cart.get_total() != initial_total

def test_remove_item_from_cart(page: Page, cart_with_item):
    """Remove item and verify cart shows empty."""
    cart = CartPage(cart_with_item)
    cart.remove_item(0)
    assert cart.is_empty()

def test_empty_cart_message(page: Page):
    """Empty cart shows appropriate message."""
    cart = CartPage(page)
    cart.navigate()
    assert cart.is_empty()
    expect(cart.empty_message).to_contain_text("Cart is empty")

def test_checkout_button_visibility(page: Page, cart_with_item):
    """Checkout button only visible with items."""
    cart = CartPage(cart_with_item)
    expect(cart.checkout_button).to_be_visible()
```

**Phase 5: Run & Debug**
```
You: Run the tests

Claude Code: pytest tests/e2e/test_cart.py -v
Results: 4 passed, 1 failed

FAILED test_cart_total_updates - AssertionError: totals are equal

You: The test is failing because the page doesn't update the total automatically. Fix it.

Claude Code: Adding page.wait_for_selector('.cart-total:not(:has-text("..."))')
after quantity update to wait for recalculation.
```

**Key learning:** Claude Code maintains context — later prompts reference earlier code automatically. It can read error messages and propose fixes.

---

### Exercise 4: API Tests — Solution

**Test structure:**
```python
# Key fixtures
@pytest.fixture
async def auth_token():
    """Get auth token for test user."""
    response = requests.post(f"{BASE_URL}/auth/login", json={
        "email": "test@example.com",
        "password": "TestPass@123"
    })
    return response.json()["token"]

@pytest.fixture
def headers(auth_token):
    return {"Authorization": f"Bearer {auth_token}"}

# Cleanup fixture
@pytest.fixture(autouse=True)
async def cleanup(created_user_ids):
    yield
    for uid in created_user_ids:
        requests.delete(f"{BASE_URL}/users/{uid}", headers=headers)
```

**Test coverage map:**

| Endpoint | Tests | Coverage |
|----------|-------|----------|
| GET /users | List, pagination, empty | 3 |
| GET /users/{id} | Found, not found | 2 |
| POST /users | Success, validation (4 params), duplicate | 6 |
| PUT /users | Success, not found, invalid | 3 |
| DELETE /users | Success, not found, no auth | 3 |
| **Total** | | **17 tests** |

---

## Common Mistakes Across All Roles

| Mistake | Role Most Affected | Fix |
|---------|-------------------|-----|
| Blindly trusting AI output | All | Apply anti-hallucination rules (Ch 1) |
| Not running generated tests | Automation | Always run before committing |
| Vague prompts to AI | QA Engineer | Use RICE POT (Ch 2) every time |
| Not referencing existing patterns | SDET | Use @codebase in Augment |
| Forgetting cleanup in API tests | Automation | Autouse fixtures for cleanup |
| Missing edge cases | SDET | Use decision tables + error guessing |

---

## Grading Rubric

| Role | Exercise Points | Total |
|------|----------------|-------|
| **QA Engineer** | Ex1: 25, Ex2: 30, Ex3: 25, Ex4: 20 | 100 |
| **SDET** | Ex1: 30, Ex2: 25, Ex3: 30, Ex4: 15 | 100 |
| **Automation** | Ex1: 20, Ex2: 25, Ex3: 20, Ex4: 20, Ex5: 15 | 100 |
