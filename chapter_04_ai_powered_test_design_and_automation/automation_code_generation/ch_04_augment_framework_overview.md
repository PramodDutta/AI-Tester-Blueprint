# Augment with Automation Frameworks

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> Augment understands your entire codebase. When combined with Playwright, it generates tests that match your existing patterns, naming conventions, and architecture — not generic templates.

---

## What You Already Know (Building on Previous Chapters)

| Chapter | Knowledge Used Here |
|---------|---------------------|
| **Chapter 1** | Anti-hallucination rules — verify Augment suggestions against real code |
| **Chapter 2** | RICE POT — structure your Augment chat prompts |
| **Chapter 3** | [Augment Setup](../../chapter_03_essential_ai_tools_setup/ide_integrations/ch_03_augment_setup.md) — already installed and indexed |

---

## Why Augment for Automation Frameworks?

| Feature | Augment Advantage |
|---------|-------------------|
| **Codebase indexing** | Understands your Page Objects, fixtures, helpers |
| **Style matching** | Generates tests matching YOUR coding style |
| **Cross-file context** | Knows about imports, dependencies, base classes |
| **Pattern learning** | Learns your assertion style, naming conventions |
| **Real-time** | Suggestions while you type, no copy-paste |

---

## Setup: Augment + Playwright Project

### Ensure Augment is Indexing Your Project

1. Open your Playwright project in VS Code
2. Augment automatically indexes all files
3. Wait for indexing to complete (status bar indicator)

### Ideal Project Structure for Augment

```
playwright-project/
├── tests/
│   ├── pages/              ← Augment learns Page Object patterns
│   │   ├── base_page.py    ← Base class Augment references
│   │   ├── login_page.py   ← Augment uses this as style template
│   │   ├── cart_page.py
│   │   └── checkout_page.py
│   ├── e2e/               ← Augment matches test patterns here
│   │   ├── test_login.py   ← First test file (style reference)
│   │   ├── test_cart.py
│   │   └── test_checkout.py
│   ├── api/               ← API test patterns
│   │   └── test_users_api.py
│   └── conftest.py        ← Augment uses fixtures automatically
├── pytest.ini
└── requirements.txt
```

---

## Workflow 1: Generate Page Object Matching Existing Style

### Context: Existing Page Objects Augment Has Learned

```python
# login_page.py (existing — Augment has indexed this)
from playwright.async_api import Page, expect
from tests.pages.base_page import BasePage


class LoginPage(BasePage):
    """Page Object for Login page."""

    def __init__(self, page: Page):
        super().__init__(page)
        self.email = page.locator('#email')
        self.password = page.locator('#password')
        self.submit_btn = page.locator('button[type="submit"]')
        self.error_msg = page.locator('.error-message')

    async def login(self, email: str, password: str):
        """Fill and submit login form."""
        await self.email.fill(email)
        await self.password.fill(password)
        await self.submit_btn.click()

    async def get_error(self) -> str:
        """Return error message text."""
        await expect(self.error_msg).to_be_visible()
        return await self.error_msg.inner_text()
```

### Augment Chat: Generate New Page Object

```text
@codebase Create a Page Object for the profile settings page at /profile/settings

Fields:
- First name input
- Last name input
- Email display (read-only)
- Avatar upload
- Save button
- Success toast message

Match the exact style and patterns used in our existing Page Objects.
```

### Augment Generates (Style-Matched)

```python
# profile_page.py
from playwright.async_api import Page, expect
from tests.pages.base_page import BasePage


class ProfilePage(BasePage):
    """Page Object for Profile Settings page."""

    def __init__(self, page: Page):
        super().__init__(page)
        self.first_name = page.locator('#first-name')
        self.last_name = page.locator('#last-name')
        self.email_display = page.locator('.email-display')
        self.avatar_upload = page.locator('input[type="file"]#avatar')
        self.save_btn = page.locator('button[type="submit"]')
        self.success_toast = page.locator('.toast.success')

    async def update_name(self, first: str, last: str):
        """Update first and last name."""
        await self.first_name.fill(first)
        await self.last_name.fill(last)

    async def upload_avatar(self, file_path: str):
        """Upload avatar image."""
        await self.avatar_upload.set_input_files(file_path)

    async def save(self):
        """Click save button."""
        await self.save_btn.click()

    async def get_success_message(self) -> str:
        """Return success toast message."""
        await expect(self.success_toast).to_be_visible()
        return await self.success_toast.inner_text()
```

Notice: Augment matched the exact pattern — `BasePage` inheritance, locator naming, method style, docstrings.

---

## Workflow 2: Generate Tests Matching Existing Test Style

### Context: Existing Test Augment Has Learned

```python
# test_login.py (existing — Augment has indexed)
import pytest
from playwright.async_api import Page, expect
from tests.pages.login_page import LoginPage

VALID_EMAIL = "testuser@example.com"
VALID_PASSWORD = "Secure@123"


@pytest.mark.asyncio
async def test_login_success(page: Page):
    """Verify successful login redirects to dashboard."""
    login = LoginPage(page)
    await login.navigate()
    await login.login(VALID_EMAIL, VALID_PASSWORD)
    await expect(page).to_have_url('**/dashboard')


@pytest.mark.asyncio
async def test_login_invalid_password(page: Page):
    """Verify invalid password shows error message."""
    login = LoginPage(page)
    await login.navigate()
    await login.login(VALID_EMAIL, "WrongPass1")
    error = await login.get_error()
    assert error == "Invalid email or password", f"Unexpected error: {error}"
```

### Augment Chat: Generate Profile Tests

```text
@codebase Generate tests for the profile update feature using ProfilePage.

Test these scenarios:
1. Update name successfully
2. Upload avatar (valid image)
3. Upload avatar (invalid file type)
4. Save without changes

Match the test style in test_login.py exactly.
Reference the conftest.py fixtures.
```

### Augment Generates (Pattern-Matched)

```python
# test_profile.py
import pytest
from playwright.async_api import Page, expect
from tests.pages.profile_page import ProfilePage

# Test Data
VALID_AVATAR = "tests/data/avatar_valid.png"
INVALID_AVATAR = "tests/data/document.pdf"


@pytest.mark.asyncio
async def test_profile_update_name(authenticated_page: Page):
    """Verify name update saves successfully."""
    profile = ProfilePage(authenticated_page)
    await profile.navigate()
    await profile.update_name("Jane", "Smith")
    await profile.save()

    message = await profile.get_success_message()
    assert message == "Profile updated successfully", f"Unexpected message: {message}"


@pytest.mark.asyncio
async def test_profile_upload_valid_avatar(authenticated_page: Page):
    """Verify valid image avatar uploads successfully."""
    profile = ProfilePage(authenticated_page)
    await profile.navigate()
    await profile.upload_avatar(VALID_AVATAR)
    await profile.save()

    message = await profile.get_success_message()
    assert message == "Profile updated successfully", f"Unexpected message: {message}"


@pytest.mark.asyncio
async def test_profile_upload_invalid_avatar(authenticated_page: Page):
    """Verify invalid file type shows validation error."""
    profile = ProfilePage(authenticated_page)
    await profile.navigate()
    await profile.upload_avatar(INVALID_AVATAR)
    await profile.save()

    error = await profile.get_error()
    assert "image" in error.lower(), f"Expected image type error, got: {error}"


@pytest.mark.asyncio
async def test_profile_save_no_changes(authenticated_page: Page):
    """Verify saving without changes shows appropriate message."""
    profile = ProfilePage(authenticated_page)
    await profile.navigate()
    await profile.save()

    message = await profile.get_success_message()
    assert message == "No changes to save", f"Unexpected message: {message}"
```

Notice: `authenticated_page` fixture used automatically (learned from conftest.py), assertion style matches exactly, test data defined at top of file.

---

## Workflow 3: Refactor Existing Tests

### Augment Chat: Find Duplication

```text
@codebase Analyze all test files in /tests/e2e/ and identify:
1. Duplicated setup code
2. Repeated assertions that could be helper methods
3. Inconsistent naming conventions
4. Missing fixture usage

Suggest specific refactoring with code examples.
```

### Augment Output

```
REFACTORING SUGGESTIONS:

1. DUPLICATION: Navigation + login repeated in 8 test files
   FIX: Use authenticated_page fixture (already in conftest.py)
   Files affected: test_cart.py, test_checkout.py, test_orders.py...

2. INCONSISTENT NAMING:
   test_cart.py uses: test_add_item_to_cart
   test_checkout.py uses: test_checkout_add_item
   FIX: Standardize to: test_{feature}_{action}

3. MISSING ASSERTIONS:
   test_checkout.py::test_payment_success only checks URL
   FIX: Add order confirmation number assertion

4. REPEATED ASSERTION PATTERN:
   "await expect(element).to_be_visible()" followed by
   "text = await element.inner_text()" appears 12 times
   FIX: Extract to BasePage.get_visible_text() method
```

---

## Workflow 4: Generate API Tests with Framework Context

```text
@codebase Generate API tests for POST /api/orders endpoint.

Reference:
- Existing API patterns in tests/api/test_users_api.py
- Auth fixture from conftest.py
- Base URL configuration

Requirements:
- Create order with valid cart items
- Create order with empty cart (should fail)
- Create order without auth (should fail 401)
```

### Augment Generates (Matching API Test Style)

```python
# tests/api/test_orders_api.py
"""API tests for Order creation endpoint."""
import pytest
import requests
from tests.api.api_client import APIClient


@pytest.fixture
def api(auth_token):
    """Create authenticated API client."""
    return APIClient(base_url="https://staging.ecommerce.com/api", token=auth_token)


def test_create_order_success(api):
    """Verify order creation with valid cart items returns 201."""
    payload = {
        "items": [
            {"product_id": 101, "quantity": 2},
            {"product_id": 102, "quantity": 1}
        ],
        "shipping_address_id": 1
    }
    response = api.post("/orders", json=payload)

    assert response.status_code == 201, f"Expected 201, got {response.status_code}"
    assert "order_id" in response.json()
    assert response.json()["status"] == "pending_payment"


def test_create_order_empty_cart(api):
    """Verify order creation with empty cart returns 400."""
    payload = {"items": [], "shipping_address_id": 1}
    response = api.post("/orders", json=payload)

    assert response.status_code == 400
    assert "empty" in response.json()["message"].lower()


def test_create_order_no_auth():
    """Verify order creation without auth returns 401."""
    client = APIClient(base_url="https://staging.ecommerce.com/api", token=None)
    payload = {"items": [{"product_id": 101, "quantity": 1}]}

    response = client.post("/orders", json=payload)
    assert response.status_code == 401
```

---

## Augment vs Claude Code Comparison

| Feature | Augment | Claude Code |
|---------|---------|-------------|
| **Environment** | VS Code (GUI) | Terminal (CLI) |
| **Codebase context** | Deep indexing | File-by-file |
| **Style matching** | Excellent | Good |
| **Real-time** | Yes (as you type) | Conversational |
| **File creation** | Via chat | Direct creation |
| **Test execution** | Via terminal | Built-in |
| **Best for** | IDE workflow | End-to-end automation |

### Recommended Combined Workflow

```
1. Use Augment in VS Code for:
   - Generating Page Objects (style matching)
   - Writing test cases (pattern matching)
   - Refactoring (cross-file analysis)

2. Use Claude Code in terminal for:
   - Project setup
   - Running and debugging tests
   - Generating reports
   - Full requirement → code pipeline
```

---

## Anti-Hallucination Check (Chapter 1)

- [ ] Verify generated locators against actual application
- [ ] Confirm Augment's style suggestions match your actual patterns
- [ ] Don't trust @codebase analysis without manual review
- [ ] Run all generated tests before adding to CI/CD
- [ ] Ensure fixture references actually exist in conftest.py

---

## Next Steps

- Practice with [Automation Tester Exercises](../learning_practice/ch_04_exercises_automation_tester.md)
- Compare both approaches in [Claude Code walkthrough](ch_04_claude_code_qa_automation.md)
- Track results with [Test Metrics](../documentation_metrics/ch_04_test_metrics_with_ai.md)
