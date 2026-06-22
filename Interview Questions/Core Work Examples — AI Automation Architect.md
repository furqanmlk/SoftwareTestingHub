# Core Work Examples — AI Automation Architect

> Practical code examples and interview talking points for each core work area.  
> Each section includes: **what it is**, **a working script example**, and **how to talk about it in an interview**.

---

## 1. Framework Development

**What it is:** Building the base test infrastructure that all other automation sits on — folder structure, config management, base classes, reporting hooks.

### Example: Playwright + Python base framework structure

```python
# conftest.py — shared fixtures for the entire framework
import pytest
from playwright.sync_api import sync_playwright

@pytest.fixture(scope="session")
def browser_context():
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=True)
        context = browser.new_context(
            base_url="https://your-app.com",
            viewport={"width": 1280, "height": 720}
        )
        yield context
        browser.close()

@pytest.fixture
def page(browser_context):
    page = browser_context.new_page()
    yield page
    page.close()
```

```python
# base_page.py — reusable page object base class
class BasePage:
    def __init__(self, page):
        self.page = page

    def navigate(self, path: str):
        self.page.goto(path)

    def wait_for_element(self, selector: str, timeout: int = 5000):
        self.page.wait_for_selector(selector, timeout=timeout)

    def take_screenshot(self, name: str):
        self.page.screenshot(path=f"reports/screenshots/{name}.png")
```

```python
# login_page.py — example page object using base class
from base_page import BasePage

class LoginPage(BasePage):
    USERNAME = "#username"
    PASSWORD = "#password"
    SUBMIT   = "button[type='submit']"

    def login(self, username: str, password: str):
        self.navigate("/login")
        self.page.fill(self.USERNAME, username)
        self.page.fill(self.PASSWORD, password)
        self.page.click(self.SUBMIT)
        self.page.wait_for_url("**/dashboard")
```

**Interview talking point:**
> "I treat the framework like a product. The key decisions I make upfront are: single base class for all page objects, centralised config via environment variables, and a shared fixture layer in conftest so no test manages its own browser lifecycle. This keeps individual tests readable and easy to maintain."

---

## 2. Self-Healing Script Tuning

**What it is:** Detecting when a locator breaks due to a UI change and automatically finding an alternative — reducing maintenance overhead dramatically.

### Example: Self-healing locator with fallback strategy (Python + Playwright)

```python
# self_healing_locator.py
from playwright.sync_api import Page
from typing import List
import logging

logger = logging.getLogger(__name__)

class SelfHealingLocator:
    """
    Tries a list of selectors in priority order.
    Logs which selector was used so you can update the primary over time.
    """

    def __init__(self, page: Page, selectors: List[str], element_name: str = "element"):
        self.page = page
        self.selectors = selectors
        self.element_name = element_name

    def find(self, timeout: int = 3000):
        for i, selector in enumerate(self.selectors):
            try:
                element = self.page.wait_for_selector(selector, timeout=timeout)
                if element:
                    if i > 0:
                        logger.warning(
                            f"[Self-Heal] '{self.element_name}' found via fallback selector "
                            f"#{i}: '{selector}'. Primary selector '{self.selectors[0]}' failed."
                        )
                    return element
            except Exception:
                continue
        raise Exception(
            f"[Self-Heal FAILED] Could not locate '{self.element_name}' "
            f"with any of {len(self.selectors)} selectors."
        )


# Usage in a test
def test_checkout_button(page):
    btn = SelfHealingLocator(
        page,
        selectors=[
            "#checkout-btn",                    # primary: ID
            "button.checkout",                  # fallback 1: class
            "button:has-text('Checkout')",      # fallback 2: text
            "[data-testid='checkout-button']",  # fallback 3: test ID
        ],
        element_name="Checkout button"
    ).find()
    btn.click()
```

**Interview talking point:**
> "Self-healing doesn't mean magic — it means graceful degradation. I define a priority stack of selectors: stable test IDs first, then semantic attributes, then text, never XPath positions. The heal log tells me which selectors are drifting so I can fix them at the source during the next sprint."

---

## 3. AI Test Generation

**What it is:** Using AI tools (or the Anthropic/OpenAI API) to generate test cases from requirements, user stories, or existing code — then reviewing and merging the good ones.

### Example: Generate Playwright tests from a user story using Claude API

```python
# ai_test_generator.py
import anthropic
import json

client = anthropic.Anthropic()  # uses ANTHROPIC_API_KEY env var

def generate_tests_from_story(user_story: str) -> str:
    """Sends a user story to Claude and gets back Playwright test code."""

    prompt = f"""
You are a senior QA automation engineer. Given this user story, write 3-5
Playwright (Python) test cases covering happy path, edge cases, and a negative test.

User story:
{user_story}

Return ONLY valid Python code using pytest and Playwright sync API.
Include comments explaining each test's intent.
"""

    message = client.messages.create(
        model="claude-sonnet-4-6",
        max_tokens=1500,
        messages=[{"role": "user", "content": prompt}]
    )
    return message.content[0].text


# Example usage
story = """
As a user, I want to log in with my email and password,
so that I can access my account dashboard.
Acceptance criteria:
- Valid credentials redirect to /dashboard
- Invalid password shows 'Incorrect password' error
- Empty fields show 'Required' validation messages
- After 5 failed attempts, the account is locked
"""

generated_code = generate_tests_from_story(story)
print(generated_code)

# Save to file for review before committing
with open("tests/generated/test_login_ai.py", "w") as f:
    f.write(generated_code)
    print("Saved to tests/generated/test_login_ai.py — review before committing.")
```

**Interview talking point:**
> "AI generation accelerates the first draft — not the final output. My process is: generate, review for logic correctness, run against a real environment, then promote to the main suite. I never auto-commit AI-generated tests. The value is cutting the blank-page problem for new feature coverage."

---

## 4. API & Integration Testing

**What it is:** Testing the service layer directly — validating request/response contracts, auth flows, error codes, and data consistency without going through the UI.

### Example: REST API test with Python + requests + pytest

```python
# test_user_api.py
import pytest
import requests

BASE_URL = "https://api.your-app.com/v1"
HEADERS  = {"Authorization": "Bearer test-token", "Content-Type": "application/json"}


@pytest.fixture
def created_user():
    """Creates a user and cleans up after the test."""
    payload = {"name": "Test User", "email": "test@example.com", "role": "viewer"}
    res = requests.post(f"{BASE_URL}/users", json=payload, headers=HEADERS)
    assert res.status_code == 201, f"Setup failed: {res.text}"
    user = res.json()
    yield user
    # Teardown
    requests.delete(f"{BASE_URL}/users/{user['id']}", headers=HEADERS)


def test_get_user_returns_correct_schema(created_user):
    res = requests.get(f"{BASE_URL}/users/{created_user['id']}", headers=HEADERS)
    assert res.status_code == 200
    data = res.json()
    assert "id" in data
    assert "email" in data
    assert "role" in data
    assert data["email"] == "test@example.com"


def test_update_user_name(created_user):
    res = requests.patch(
        f"{BASE_URL}/users/{created_user['id']}",
        json={"name": "Updated Name"},
        headers=HEADERS
    )
    assert res.status_code == 200
    assert res.json()["name"] == "Updated Name"


def test_unauthorized_access_returns_401():
    res = requests.get(f"{BASE_URL}/users", headers={"Authorization": "Bearer invalid"})
    assert res.status_code == 401
    assert "Unauthorized" in res.json().get("message", "")


def test_create_user_with_missing_field_returns_400():
    res = requests.post(
        f"{BASE_URL}/users",
        json={"name": "No Email User"},  # missing required 'email'
        headers=HEADERS
    )
    assert res.status_code == 400
```

**Interview talking point:**
> "API tests are my highest-value layer — they run in seconds, don't break on UI redesigns, and catch contract regressions early. I always test the 400/401/422 cases as hard as the happy path. The fixture pattern for setup/teardown keeps tests independent and the database clean."

---

## 5. Agentic Workflow Iteration

**What it is:** Building multi-step autonomous test agents that can plan, execute, observe results, and decide next actions — going beyond scripted test sequences.

### Example: Simple agentic test loop using Claude API with tool use

```python
# agentic_test_agent.py
import anthropic
import json

client = anthropic.Anthropic()

# Define tools the agent can call
tools = [
    {
        "name": "run_test",
        "description": "Execute a named test case and return the result",
        "input_schema": {
            "type": "object",
            "properties": {
                "test_name": {"type": "string", "description": "Name of the test to run"},
            },
            "required": ["test_name"]
        }
    },
    {
        "name": "get_test_list",
        "description": "Get list of all available tests for a given feature",
        "input_schema": {
            "type": "object",
            "properties": {
                "feature": {"type": "string", "description": "Feature area to get tests for"},
            },
            "required": ["feature"]
        }
    }
]


def mock_run_test(test_name: str) -> dict:
    """Simulates running a test — replace with real pytest/subprocess call."""
    results = {
        "test_login_valid":   {"status": "passed",  "duration_ms": 340},
        "test_login_invalid": {"status": "passed",  "duration_ms": 210},
        "test_login_locked":  {"status": "failed",  "duration_ms": 890, "error": "Expected 403, got 200"},
    }
    return results.get(test_name, {"status": "not_found"})


def mock_get_test_list(feature: str) -> list:
    tests = {
        "login": ["test_login_valid", "test_login_invalid", "test_login_locked"]
    }
    return tests.get(feature, [])


def run_agentic_session(goal: str):
    print(f"\n🤖 Agent goal: {goal}\n")
    messages = [{"role": "user", "content": goal}]

    while True:
        response = client.messages.create(
            model="claude-sonnet-4-6",
            max_tokens=1000,
            tools=tools,
            messages=messages
        )

        if response.stop_reason == "end_turn":
            print("\n✅ Agent completed:")
            print(response.content[0].text)
            break

        # Handle tool calls
        tool_results = []
        for block in response.content:
            if block.type == "tool_use":
                print(f"  → Calling tool: {block.name}({block.input})")
                if block.name == "run_test":
                    result = mock_run_test(block.input["test_name"])
                elif block.name == "get_test_list":
                    result = mock_get_test_list(block.input["feature"])
                else:
                    result = {"error": "unknown tool"}

                tool_results.append({
                    "type": "tool_result",
                    "tool_use_id": block.id,
                    "content": json.dumps(result)
                })

        messages.append({"role": "assistant", "content": response.content})
        messages.append({"role": "user",      "content": tool_results})


# Run it
run_agentic_session(
    "Run all tests for the login feature and give me a summary of results. "
    "Highlight any failures and suggest what might be wrong."
)
```

**Interview talking point:**
> "Agentic testing is where I see the biggest future — instead of a fixed script, you give the agent a goal: 'validate the checkout flow end-to-end'. It plans the steps, runs tools, observes failures, and decides whether to retry or escalate. We're early here, but I've prototyped it with Claude's tool-use API and it meaningfully reduces test script maintenance for exploratory coverage."

---

## 6. Intelligent Test Selection & Optimization

**What it is:** Using ML or heuristics to decide which subset of tests to run for a given code change — cutting suite time from hours to minutes without sacrificing confidence.

### Example: Risk-based test selector using file change mapping (Python)

```python
# intelligent_test_selector.py
import subprocess
import json
from pathlib import Path

# Map: source file pattern → tests that cover it
COVERAGE_MAP = {
    "src/auth":        ["tests/test_login.py",    "tests/test_session.py"],
    "src/cart":        ["tests/test_cart.py",      "tests/test_checkout.py"],
    "src/payments":    ["tests/test_checkout.py",  "tests/test_refunds.py"],
    "src/user_profile":["tests/test_profile.py"],
    "src/api":         ["tests/test_api_users.py", "tests/test_api_orders.py"],
}

# Tests that always run regardless of changes (smoke suite)
ALWAYS_RUN = ["tests/test_smoke.py"]


def get_changed_files(base_branch: str = "main") -> list:
    """Get files changed vs the base branch via git diff."""
    result = subprocess.run(
        ["git", "diff", "--name-only", base_branch],
        capture_output=True, text=True
    )
    return result.stdout.strip().split("\n")


def select_tests(changed_files: list) -> list:
    selected = set(ALWAYS_RUN)

    for changed_file in changed_files:
        for source_pattern, tests in COVERAGE_MAP.items():
            if source_pattern in changed_file:
                selected.update(tests)

    return sorted(selected)


def main():
    changed = get_changed_files("main")
    print(f"Changed files ({len(changed)}):")
    for f in changed:
        print(f"  {f}")

    tests_to_run = select_tests(changed)
    print(f"\nSelected {len(tests_to_run)} test files to run:")
    for t in tests_to_run:
        print(f"  ✓ {t}")

    # Output for CI consumption
    with open("selected_tests.json", "w") as f:
        json.dump({"tests": tests_to_run}, f, indent=2)
    print("\nSaved to selected_tests.json for CI pipeline.")


if __name__ == "__main__":
    main()
```

```yaml
# .github/workflows/smart-test.yml — CI consuming the selector output
name: Smart Test Run

on: [pull_request]

jobs:
  select-and-run:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Select tests based on changes
        run: python intelligent_test_selector.py

      - name: Run selected tests
        run: |
          TESTS=$(python -c "import json; d=json.load(open('selected_tests.json')); print(' '.join(d['tests']))")
          pytest $TESTS --tb=short -q
```

**Interview talking point:**
> "The simplest form of intelligent selection is a static coverage map — you know which modules each test covers, so you only run what's relevant to the PR. More advanced versions use actual code coverage data or ML models trained on historical failure patterns. Even the simple version typically cuts CI time by 60–70% on large repos."

---

## Summary Table

| Core Work Area | Script Needed? | Primary Tools | Interview Complexity |
|---|:---:|---|:---:|
| Framework development | ✅ Yes | Playwright, pytest, Python | Medium |
| Self-healing scripts | ✅ Yes | Playwright, custom locator logic | Medium |
| AI test generation | ✅ Yes | Claude API, Anthropic SDK | High |
| API & integration testing | ✅ Yes | requests, pytest, REST Assured | Medium |
| Agentic workflow | ✅ Yes | Claude API (tool use), multi-step agents | High |
| Intelligent test selection | ✅ Yes | Python, Git, GitHub Actions | Medium-High |

---

*All examples use Python. Java equivalents available for Selenium/TestNG — raise as a follow-up.*  
*Last updated: June 2026*
