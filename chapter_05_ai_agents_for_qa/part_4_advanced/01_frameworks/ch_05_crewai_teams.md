# CrewAI Teams for QA

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

CrewAI makes it easy to create teams of AI agents that collaborate on tasks.

---

## 📦 Installation

```bash
pip install crewai crewai-tools
```

---

## 🛠️ QA Team Example

```python
from crewai import Agent, Task, Crew, Process
from crewai_tools import FileReadTool

# Define agents
requirements_analyst = Agent(
    role="Requirements Analyst",
    goal="Analyze requirements and identify testable scenarios",
    backstory="Expert at extracting test scenarios from requirements",
    llm="claude-3-5-sonnet-20241022"
)

test_writer = Agent(
    role="Test Case Writer",
    goal="Write comprehensive test cases with clear steps",
    backstory="Experienced QA engineer with attention to detail",
    llm="claude-3-5-sonnet-20241022"
)

test_reviewer = Agent(
    role="Test Reviewer",
    goal="Review test cases for completeness and edge cases",
    backstory="Senior QA lead focused on quality and coverage",
    llm="claude-3-5-sonnet-20241022"
)

# Define tasks
analyze_task = Task(
    description="Analyze the following requirement and identify all testable scenarios: {requirement}",
    expected_output="List of testable scenarios with priority",
    agent=requirements_analyst
)

write_task = Task(
    description="Write detailed test cases for the identified scenarios",
    expected_output="Complete test cases with steps, expected results, and test data",
    agent=test_writer,
    context=[analyze_task]
)

review_task = Task(
    description="Review the test cases and suggest improvements",
    expected_output="Review comments and final approved test cases",
    agent=test_reviewer,
    context=[write_task]
)

# Create crew
qa_crew = Crew(
    agents=[requirements_analyst, test_writer, test_reviewer],
    tasks=[analyze_task, write_task, review_task],
    process=Process.sequential,
    verbose=True
)

# Run the crew
result = qa_crew.kickoff(inputs={
    "requirement": """
    As a user, I want to reset my password via email
    so that I can regain access if I forget my password.
    
    Acceptance Criteria:
    - User can request password reset from login page
    - Email is sent within 30 seconds
    - Reset link expires after 24 hours
    - New password must meet security requirements
    """
})

print(result)
```

---

## 📊 Output Example

```markdown
## Analysis (Requirements Analyst)
Identified 8 testable scenarios:
1. Valid email receives reset link (P0)
2. Invalid email shows error (P1)
3. Email delivery timing (P1)
4. Link expiration validation (P0)
...

## Test Cases (Test Writer)
TC-001: Valid Password Reset Request
- Precondition: User exists with email user@test.com
- Steps: ...
- Expected: Reset email received within 30s

TC-002: Invalid Email Handling
...

## Review (Test Reviewer)
✅ Approved with suggestions:
- Add test for special characters in email
- Add concurrent reset request test
- Consider password history validation
```

---

## 🔧 Adding Custom Tools

```python
from crewai_tools import tool

@tool("run_playwright_test")
def run_playwright_test(test_file: str) -> str:
    """Run a Playwright test file and return results."""
    import subprocess
    result = subprocess.run(
        ["npx", "playwright", "test", test_file],
        capture_output=True,
        text=True
    )
    return result.stdout

automation_engineer = Agent(
    role="Automation Engineer",
    goal="Execute automated tests",
    tools=[run_playwright_test],
    llm="claude-3-5-sonnet-20241022"
)
```

---

## 📚 See Also

- [Frameworks Overview](ch_05_frameworks_overview.md)
- [Multi-Agent Systems](../../part_1_fundamentals/multi_agent_systems/ch_05_multi_agent_overview.md)
