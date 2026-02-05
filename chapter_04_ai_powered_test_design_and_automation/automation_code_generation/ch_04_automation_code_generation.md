# Automation Code Generation with AI

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> This is where AI delivers the biggest time savings in QA. Generate production-ready Playwright test scripts from requirements, manual test cases, or even just a description — in seconds.

---

## What You Already Know (Building on Previous Chapters)

| Chapter | Knowledge Used Here |
|---------|---------------------|
| **Chapter 1** | Anti-hallucination — always verify generated selectors and assertions |
| **Chapter 2** | RICE POT framework — structure prompts for code generation |
| **Chapter 3** | Tools — GitHub Copilot, Anti Gravity, Claude Code, VS Code setup |

---

## Framework: Playwright (Python)

### Why Playwright?

| Feature | Playwright | Selenium |
|---------|------------|----------|
| Speed | Faster | Slower |
| Browser support | Chromium, Firefox, WebKit | Chrome, Firefox, Edge |
| Auto-waiting | Yes (built-in) | No (manual waits) |
| Network interception | Yes | Limited |
| Mobile emulation | Yes | Limited |
| Setup complexity | Simple | Moderate |

### Setup

```bash
pip install playwright pytest pytest-playwright
playwright install
```

---

## Code Generation Patterns

### Pattern 1: Comment → Code (Copilot / Anti Gravity)

Write a descriptive comment, AI generates the code:

```python
# Test: User successfully registers with valid details,
# verifies email confirmation page is shown, and account appears in database

def test_user_registration_success(page: Page):
    # AI generates complete test from the comment above
```

### Pattern 2: Description → Full Test (Claude / ChatGPT)

Send a description, get a complete test file back:

```text
Generate a Playwright Python test for user registration:
- Navigate to /register
- Fill name, email, password
- Submit form
- Verify success page
- Verify user exists via API
```

### Pattern 3: Manual Test → Automated (AI Conversion)

Convert existing manual test case to code:

```text
Convert this manual test to Playwright Python:

TC-101: Register with valid details
1. Open https://staging.ecommerce.com/register
2. Enter Name: "John Doe"
3. Enter Email: "john@test.com"
4. Enter Password: "Secure@123"
5. Click "Register"
6. Verify page shows "Registration Successful"
```

---

## RICE POT Prompt for Playwright Code Generation

```text
Role: Senior Automation Engineer using Playwright with Python

Intent: Generate a complete Playwright test file for the given feature

Context:
- Framework: Playwright with pytest
- Pattern: Page Object Model
- Application: E-Commerce Platform (https://staging.ecommerce.com)
- Feature: User Login and Dashboard Access

Requirements:
- Valid login redirects to dashboard
- Invalid password shows error
- Account lockout after 3 failed attempts
- "Remember Me" persists session

Expected Output: Complete test file with Page Object + test functions

Parameters:
- Use async Playwright
- Include explicit assertions with messages
- Use fixtures for browser setup/teardown
- Add parameterized tests where applicable
- Follow PEP 8 style

Output Format:
# login_page.py (Page Object)
# test_login.py (Test file)
# conftest.py (Fixtures)

Task: Generate all three files now.
```

---

## Generated Code: Page Object

```python
# login_page.py
"""Page Object for Login functionality."""

from playwright.async_api import Page, expect


class LoginPage:
    """Page Object Model for the Login page."""

    def __init__(self, page: Page):
        self.page = page
        # Locators
        self.email_input = page.locator('#email')
        self.password_input = page.locator('#password')
        self.remember_me_checkbox = page.locator('#remember-me')
        self.submit_button = page.locator('button[type="submit"]')
        self.error_message = page.locator('.error-message')
        self.lockout_message = page.locator('.lockout-message')

    async def navigate(self):
        """Navigate to login page."""
        await self.page.goto('https://staging.ecommerce.com/login')

    async def fill_credentials(self, email: str, password: str):
        """Fill in login credentials."""
        await self.email_input.fill(email)
        await self.password_input.fill(password)

    async def check_remember_me(self):
        """Check the Remember Me checkbox."""
        await self.remember_me_checkbox.check()

    async def submit(self):
        """Click the login submit button."""
        await self.submit_button.click()

    async def get_error_message(self) -> str:
        """Get the error message text if displayed."""
        await expect(self.error_message).to_be_visible()
        return await self.error_message.inner_text()

    async def is_locked_out(self) -> bool:
        """Check if lockout message is displayed."""
        return await self.lockout_message.is_visible()
```

---

## Generated Code: Test File

```python
# test_login.py
"""Tests for user login functionality."""

import pytest
from playwright.async_api import Page, expect
from pages.login_page import LoginPage


# --- Test Data ---
VALID_EMAIL = "testuser@example.com"
VALID_PASSWORD = "Secure@123"
INVALID_PASSWORD = "WrongPass1"
UNREGISTERED_EMAIL = "notregistered@example.com"


# --- Test: Successful Login ---
@pytest.mark.asyncio
async def test_login_valid_credentials(page: Page):
    """Test that valid credentials successfully log in the user."""
    login = LoginPage(page)
    await login.navigate()
    await login.fill_credentials(VALID_EMAIL, VALID_PASSWORD)
    await login.submit()

    # Verify redirect to dashboard
    await expect(page).to_have_url('https://staging.ecommerce.com/dashboard')
    await expect(page.locator('h1.welcome')).to_have_text('Welcome back!')


# --- Test: Invalid Password ---
@pytest.mark.asyncio
async def test_login_invalid_password(page: Page):
    """Test that invalid password shows appropriate error message."""
    login = LoginPage(page)
    await login.navigate()
    await login.fill_credentials(VALID_EMAIL, INVALID_PASSWORD)
    await login.submit()

    # Verify error message
    error = await login.get_error_message()
    assert error == "Invalid email or password", f"Expected error message, got: {error}"

    # Verify still on login page
    await expect(page).to_have_url('https://staging.ecommerce.com/login')


# --- Test: Unregistered Email ---
@pytest.mark.asyncio
async def test_login_unregistered_email(page: Page):
    """Test that unregistered email shows error."""
    login = LoginPage(page)
    await login.navigate()
    await login.fill_credentials(UNREGISTERED_EMAIL, "AnyPass123")
    await login.submit()

    error = await login.get_error_message()
    assert error == "Invalid email or password"


# --- Test: Account Lockout After 3 Failed Attempts ---
@pytest.mark.asyncio
async def test_login_account_lockout(page: Page):
    """Test that account locks after 3 consecutive failed login attempts."""
    login = LoginPage(page)
    await login.navigate()

    # Attempt 3 failed logins
    for i in range(3):
        await login.fill_credentials(VALID_EMAIL, INVALID_PASSWORD)
        await login.submit()
        # Wait for error before next attempt
        await login.get_error_message()

    # Verify lockout
    assert await login.is_locked_out(), "Account should be locked after 3 failed attempts"
    await expect(login.lockout_message).to_contain_text("locked")


# --- Test: Remember Me Persistence ---
@pytest.mark.asyncio
async def test_login_remember_me(page: Page):
    """Test that Remember Me checkbox persists the session."""
    login = LoginPage(page)
    await login.navigate()
    await login.fill_credentials(VALID_EMAIL, VALID_PASSWORD)
    await login.check_remember_me()
    await login.submit()

    # Verify on dashboard
    await expect(page).to_have_url('https://staging.ecommerce.com/dashboard')

    # Close and reopen (simulate by navigating away and back)
    await page.goto('https://staging.ecommerce.com')

    # Should still be logged in
    await expect(page).to_have_url('https://staging.ecommerce.com/dashboard')


# --- Test: Parameterized Invalid Inputs ---
@pytest.mark.parametrize("email,password,expected_error", [
    ("", VALID_PASSWORD, "Email is required"),
    (VALID_EMAIL, "", "Password is required"),
    ("invalid-email", VALID_PASSWORD, "Please enter a valid email"),
    ("a@b.c", VALID_PASSWORD, "Please enter a valid email"),
])
@pytest.mark.asyncio
async def test_login_input_validation(page: Page, email: str, password: str, expected_error: str):
    """Test login form validation with various invalid inputs."""
    login = LoginPage(page)
    await login.navigate()
    await login.fill_credentials(email, password)
    await login.submit()

    error = await login.get_error_message()
    assert error == expected_error, f"Expected '{expected_error}', got '{error}'"
```

---

## Generated Code: Fixtures

> **Note:** The `pytest-playwright` plugin provides built-in `page`, `browser`, and `context` fixtures. Use custom fixtures only when you need additional setup like authentication.

```python
# conftest.py
"""Shared fixtures for Playwright tests."""

import os
import pytest
from playwright.sync_api import Page

# --- Environment Configuration ---
# Load from environment or use defaults
BASE_URL = os.getenv("BASE_URL", "https://staging.ecommerce.com")
TEST_USER_EMAIL = os.getenv("TEST_USER_EMAIL", "testuser@example.com")
TEST_USER_PASSWORD = os.getenv("TEST_USER_PASSWORD", "Secure@123")


@pytest.fixture(scope="session")
def browser_context_args(browser_context_args):
    """Extend default browser context with custom viewport."""
    return {
        **browser_context_args,
        "viewport": {"width": 1280, "height": 720},
        "base_url": BASE_URL,
    }


@pytest.fixture
def authenticated_page(page: Page) -> Page:
    """Return a page that is already logged in."""
    from pages.login_page import LoginPage

    login = LoginPage(page)
    login.navigate()
    login.fill_credentials(TEST_USER_EMAIL, TEST_USER_PASSWORD)
    login.submit()
    page.wait_for_url("**/dashboard")
    return page


# --- Test Data Cleanup ---
@pytest.fixture
def test_user_email():
    """Generate unique test email for each test."""
    import uuid
    return f"test_{uuid.uuid4().hex[:8]}@example.com"


@pytest.fixture(autouse=True)
def cleanup_test_data(request):
    """Cleanup test data after each test (if needed)."""
    created_resources = []

    def track_resource(resource_type, resource_id):
        created_resources.append((resource_type, resource_id))

    request.node.track_resource = track_resource
    yield

    # Cleanup after test
    for resource_type, resource_id in created_resources:
        # Add cleanup logic per resource type
        pass  # e.g., delete_user(resource_id)
```

### Environment Configuration (pytest.ini)

```ini
# pytest.ini
[pytest]
base_url = https://staging.ecommerce.com
asyncio_mode = auto
addopts = -v --tb=short
markers =
    smoke: Quick sanity tests (run with -m smoke)
    regression: Full regression suite
    slow: Long-running tests
testpaths = tests

# For debugging: add --headed --slowmo=500
```

### Multi-Browser & Device Configuration

```python
# conftest.py - Browser matrix testing

import pytest

# Run tests across multiple browsers
@pytest.fixture(scope="session", params=["chromium", "firefox", "webkit"])
def browser_type(request, playwright):
    """Parametrize tests to run on all browsers."""
    return getattr(playwright, request.param)


# Mobile device emulation
@pytest.fixture
def mobile_page(playwright, browser):
    """Page configured for iPhone 13."""
    iphone = playwright.devices["iPhone 13"]
    context = browser.new_context(**iphone)
    page = context.new_page()
    yield page
    context.close()


# Slow network simulation
@pytest.fixture
def slow_network_page(browser):
    """Simulate 3G network conditions."""
    context = browser.new_context()
    page = context.new_page()
    # Throttle network
    client = page.context.new_cdp_session(page)
    client.send("Network.emulateNetworkConditions", {
        "offline": False,
        "downloadThroughput": 500 * 1024 / 8,  # 500 kbps
        "uploadThroughput": 500 * 1024 / 8,
        "latency": 400  # 400ms latency
    })
    yield page
    context.close()
```

**Running browser matrix:**
```bash
# Run on all browsers
pytest tests/ --browser chromium --browser firefox --browser webkit

# Run on specific device
pytest tests/ --device "iPhone 13"
```

### Using .env for Secrets

```bash
# .env (add to .gitignore!)
BASE_URL=https://staging.ecommerce.com
TEST_USER_EMAIL=testuser@example.com
TEST_USER_PASSWORD=Secure@123
STRIPE_TEST_KEY=sk_test_xxxx
```

```python
# Load .env in conftest.py
from dotenv import load_dotenv
load_dotenv()
```

---

---

## Playwright Codegen: Record Tests Without Writing Code

Before using AI to generate tests, consider Playwright's built-in recording tool:

```bash
# Record browser actions and generate test code
playwright codegen https://staging.ecommerce.com

# Record with specific viewport
playwright codegen --viewport-size=1280,720 https://staging.ecommerce.com

# Record for mobile
playwright codegen --device="iPhone 13" https://staging.ecommerce.com

# Save to file
playwright codegen --output=tests/e2e/test_recorded.py https://staging.ecommerce.com
```

### When to Use Codegen vs AI

| Scenario | Use Codegen | Use AI |
|----------|-------------|--------|
| Learning element selectors | ✅ | |
| Quick prototype tests | ✅ | |
| Complex business logic | | ✅ |
| Parametrized tests | | ✅ |
| Page Object generation | | ✅ |
| Test design from requirements | | ✅ |

**Pro Tip:** Use codegen to discover selectors, then feed those selectors to AI for structured test generation.

---

## Test Data Management

### The Problem

Tests need data. Bad data management causes:
- Flaky tests (data collision between tests)
- Test pollution (one test affects another)
- Environment dependency (works on staging, fails on CI)

### Solution: Isolated Test Data

```python
# conftest.py - Test data fixtures

import uuid
import pytest
import requests

BASE_URL = "https://staging.ecommerce.com/api"


@pytest.fixture
def unique_user_data():
    """Generate unique user data for each test."""
    unique_id = uuid.uuid4().hex[:8]
    return {
        "name": f"Test User {unique_id}",
        "email": f"test_{unique_id}@example.com",
        "password": "TestPass@123"
    }


@pytest.fixture
def created_user(unique_user_data, auth_headers):
    """Create a test user and clean up after test."""
    # Setup: Create user
    response = requests.post(
        f"{BASE_URL}/users",
        json=unique_user_data,
        headers=auth_headers
    )
    user = response.json()

    yield user  # Test runs here

    # Teardown: Delete user
    requests.delete(
        f"{BASE_URL}/users/{user['id']}",
        headers=auth_headers
    )


@pytest.fixture
def product_in_cart(authenticated_page, created_user):
    """Setup: User with a product in cart."""
    # Add product to cart via API (faster than UI)
    requests.post(
        f"{BASE_URL}/cart/items",
        json={"product_id": 101, "quantity": 1},
        headers={"Authorization": f"Bearer {created_user['token']}"}
    )
    yield
    # Teardown handled by created_user fixture
```

### Database Seeding for CI/CD

```python
# tests/fixtures/seed_data.py
"""Seed data for test database."""

SEED_USERS = [
    {"id": 1, "email": "admin@test.com", "role": "admin"},
    {"id": 2, "email": "user@test.com", "role": "user"},
]

SEED_PRODUCTS = [
    {"id": 101, "name": "Test Product", "price": 29.99},
    {"id": 102, "name": "Premium Product", "price": 99.99},
]

def seed_database(db_connection):
    """Run before test suite to ensure consistent data."""
    for user in SEED_USERS:
        db_connection.execute("INSERT OR IGNORE INTO users ...", user)
    for product in SEED_PRODUCTS:
        db_connection.execute("INSERT OR IGNORE INTO products ...", product)
```

---

## API Test Generation

### Prompt

```text
Generate pytest tests for REST API:

Endpoint: POST /api/users
Base URL: https://staging.ecommerce.com/api

Request Body:
{
  "name": "string (required, max 100 chars)",
  "email": "string (required, valid email)",
  "password": "string (required, min 8 chars)"
}

Responses:
- 201: User created successfully
- 400: Invalid input
- 409: Email already exists
- 500: Server error

Include: fixtures, parametrize, assertions on response body
```

### AI-Generated API Tests

```python
# test_api_users.py
"""API tests for User creation endpoint."""

import pytest
import requests

BASE_URL = "https://staging.ecommerce.com/api"


@pytest.fixture
def headers():
    """Return common headers."""
    return {"Content-Type": "application/json"}


# --- Success Case ---
def test_create_user_success(headers):
    """Test successful user creation returns 201."""
    payload = {
        "name": "John Doe",
        "email": "newuser@test.com",
        "password": "Secure@123"
    }

    response = requests.post(f"{BASE_URL}/users", json=payload, headers=headers)

    assert response.status_code == 201, f"Expected 201, got {response.status_code}"
    body = response.json()
    assert "id" in body, "Response missing 'id' field"
    assert body["email"] == payload["email"]
    assert "password" not in body, "Password should not be in response"


# --- Validation Errors ---
@pytest.mark.parametrize("payload,expected_error", [
    ({"name": "", "email": "a@b.com", "password": "Secure@1"}, "Name is required"),
    ({"name": "John", "email": "invalid", "password": "Secure@1"}, "Invalid email format"),
    ({"name": "John", "email": "a@b.com", "password": "short"}, "Password must be at least 8 characters"),
    ({"email": "a@b.com", "password": "Secure@1"}, "Name is required"),
])
def test_create_user_validation(headers, payload, expected_error):
    """Test user creation with invalid input."""
    response = requests.post(f"{BASE_URL}/users", json=payload, headers=headers)

    assert response.status_code == 400
    assert expected_error in response.json().get("message", "")


# --- Conflict ---
def test_create_user_duplicate_email(headers):
    """Test creating user with existing email returns 409."""
    payload = {
        "name": "Duplicate User",
        "email": "existing@test.com",  # Pre-existing in test DB
        "password": "Secure@123"
    }

    response = requests.post(f"{BASE_URL}/users", json=payload, headers=headers)

    assert response.status_code == 409
    assert "already exists" in response.json().get("message", "").lower()
```

---

---

## CI/CD Integration: GitHub Actions Example

```yaml
# .github/workflows/playwright.yml
name: Playwright Tests

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          playwright install --with-deps chromium

      - name: Run smoke tests
        run: pytest tests/ -m smoke -v --tb=short
        env:
          BASE_URL: ${{ secrets.STAGING_URL }}
          TEST_USER_EMAIL: ${{ secrets.TEST_USER_EMAIL }}
          TEST_USER_PASSWORD: ${{ secrets.TEST_USER_PASSWORD }}

      - name: Run full regression (on main only)
        if: github.ref == 'refs/heads/main'
        run: pytest tests/ -v --html=report.html --self-contained-html

      - name: Upload test report
        uses: actions/upload-artifact@v4
        if: always()
        with:
          name: playwright-report
          path: report.html
          retention-days: 7
```

### Running Tests in Docker

```dockerfile
# Dockerfile.test
FROM mcr.microsoft.com/playwright/python:v1.40.0-jammy

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY tests/ tests/
COPY pytest.ini .

CMD ["pytest", "tests/", "-v", "--tb=short"]
```

```bash
# Build and run
docker build -f Dockerfile.test -t playwright-tests .
docker run -e BASE_URL=https://staging.ecommerce.com playwright-tests
```

---

## Code Generation Best Practices

### Do
- [ ] Always verify generated selectors against actual DOM
- [ ] Run generated tests before adding to suite
- [ ] Add meaningful assertion messages
- [ ] Use Page Object Model for UI tests
- [ ] Include both positive and negative tests

### Don't
- [ ] Don't use hardcoded `time.sleep()` — Playwright has auto-wait
- [ ] Don't trust AI-generated selectors blindly
- [ ] Don't skip the `conftest.py` fixtures
- [ ] Don't generate tests without checking requirements first
- [ ] Don't ignore anti-hallucination rules from Chapter 1

---

## Anti-Hallucination Check (Chapter 1)

- [ ] Selectors verified against actual application DOM
- [ ] URLs are real staging/test URLs, not made-up
- [ ] Assertion values match actual expected behavior
- [ ] API endpoints exist and match your spec
- [ ] Test data is valid for your test database

---

## Next Steps

- Use [Claude Code](ch_04_claude_code_qa_automation.md) for end-to-end walkthrough: req → code → run
- Try [Augment](ch_04_augment_framework_overview.md) for IDE-based framework generation
- Practice in [Automation Tester Exercises](../learning_practice/ch_04_exercises_automation_tester.md)
