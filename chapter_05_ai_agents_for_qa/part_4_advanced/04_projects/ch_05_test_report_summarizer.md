# Test Report Summarizer Project

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Project Overview

Generate executive summaries from test reports automatically.

---

## 📋 Features

- Parse test results (JUnit XML, JSON)
- Generate executive summary
- Identify trends and risks
- Create visualizations
- Send to Slack/Email

---

## 🛠️ Implementation

```python
import xml.etree.ElementTree as ET
from langchain_anthropic import ChatAnthropic

def parse_junit_xml(xml_path: str) -> dict:
    """Parse JUnit XML report."""
    tree = ET.parse(xml_path)
    root = tree.getroot()
    
    tests = int(root.get('tests', 0))
    failures = int(root.get('failures', 0))
    errors = int(root.get('errors', 0))
    skipped = int(root.get('skipped', 0))
    
    failed_tests = []
    for testcase in root.iter('testcase'):
        if testcase.find('failure') is not None:
            failed_tests.append({
                'name': testcase.get('name'),
                'class': testcase.get('classname'),
                'message': testcase.find('failure').get('message')
            })
    
    return {
        'total': tests,
        'passed': tests - failures - errors,
        'failed': failures + errors,
        'skipped': skipped,
        'pass_rate': (tests - failures - errors) / tests * 100,
        'failed_tests': failed_tests
    }

def generate_summary(results: dict) -> str:
    """Generate executive summary."""
    llm = ChatAnthropic(model="claude-3-5-sonnet-20241022")
    
    prompt = f"""
    Generate an executive test summary:
    
    Results: {results}
    
    Include:
    1. Overall health status (emoji)
    2. Key metrics
    3. Critical failures (if any)
    4. Recommendations
    
    Keep it concise (max 200 words).
    """
    
    return llm.invoke(prompt).content

# Example usage
results = parse_junit_xml("test-results.xml")
summary = generate_summary(results)
print(summary)
```

---

## 📊 Example Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  TEST SUMMARY - Build #1234
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🟢 OVERALL: HEALTHY

📊 METRICS
  Total: 245  |  Passed: 240  |  Failed: 3  |  Skipped: 2
  Pass Rate: 98.0%

⚠️ FAILURES
  1. test_payment_timeout - Payment API slow
  2. test_login_safari - Safari compatibility
  3. test_export_large - Memory exceeded

💡 RECOMMENDATIONS
  - Investigate payment API latency
  - Add Safari to regular testing
  - Increase memory for export tests

✅ RELEASE READINESS: GO (with monitoring)
```

---

## 📚 See Also

- [Reporting Agents](../../part_1_fundamentals/agent_types_for_qa/ch_05_reporting_agents.md)
- [Slack Integration](../integrations/ch_05_slack_integration.md)
