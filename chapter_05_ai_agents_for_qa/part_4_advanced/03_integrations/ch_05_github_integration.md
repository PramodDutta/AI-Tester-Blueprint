# GitHub Integration

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Integrate agents with GitHub for code access and PR workflows.

---

## 📦 Setup

```bash
pip install PyGithub
```

---

## 🛠️ Basic Operations

```python
from github import Github

# Connect
gh = Github("your_access_token")
repo = gh.get_repo("owner/repo")

# Read file
def read_file(path: str) -> str:
    content = repo.get_contents(path)
    return content.decoded_content.decode()

# Get PR files
def get_pr_changes(pr_number: int):
    pr = repo.get_pull(pr_number)
    return [f.filename for f in pr.get_files()]

# Create comment
def comment_on_pr(pr_number: int, comment: str):
    pr = repo.get_pull(pr_number)
    pr.create_issue_comment(comment)
```

---

## 🔧 Agent for PR Review

```python
def review_pr_for_tests(pr_number: int):
    """Check if PR has test coverage."""
    files = get_pr_changes(pr_number)
    
    source_files = [f for f in files if f.endswith('.py') and 'test' not in f]
    test_files = [f for f in files if 'test' in f]
    
    if source_files and not test_files:
        comment_on_pr(pr_number, "⚠️ This PR modifies source files but has no test changes.")
```

---

## 📚 See Also

- [Jira Integration](ch_05_jira_integration.md)
- [CI/CD Integration](ch_05_cicd_integration.md)
