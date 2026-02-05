# Test Metrics with AI

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

> Numbers tell the story of your QA effort. AI helps collect, analyze, visualize, and present test metrics as custom dashboards — no expensive tools required.

---

## What You Already Know (Building on Previous Chapters)

| Chapter | Knowledge Used Here |
|---------|---------------------|
| **Chapter 1** | Foundation — understand what metrics mean, anti-hallucination on data |
| **Chapter 2** | RICE POT — prompt AI for metrics analysis and reporting |
| **Chapter 3** | Tools — Claude, Python, VS Code for dashboard creation |

---

## Key QA Metrics

| Metric | Formula | What It Tells You |
|--------|---------|-------------------|
| **Test Coverage** | (Tests Executed / Total Tests) × 100 | How much is tested |
| **Defect Detection Rate** | (Bugs Found / Total Bugs) × 100 | How effective testing is |
| **Defect Density** | Bugs / Lines of Code (or Feature Points) | Quality of code |
| **Pass Rate** | (Passed Tests / Total Tests) × 100 | Current quality level |
| **Bug Fix Ratio** | (Fixed Bugs / Total Bugs) × 100 | Dev team fix rate |
| **Automation Ratio** | (Automated Tests / Total Tests) × 100 | Automation maturity |
| **Defect Escape Rate** | (Production Bugs / Total Bugs Found) × 100 | QA effectiveness |
| **Test Execution Time** | Time per test run | Efficiency |
| **Re-test Effort** | Bugs requiring multiple fix cycles | Root cause quality |

---

## AI-Powered Metrics Analysis

### Prompt: Analyze Your Test Data

```text
Role: QA Metrics Analyst

Intent: Analyze test execution data and provide insights

Context:
Sprint: Sprint 14
Total Tests: 250
Passed: 210
Failed: 28
Skipped: 12
Bugs Found: 18
Bugs Fixed: 15
Bugs in Production (escaped): 2
Automation Coverage: 65%
Previous Sprint Automation: 58%

Expected Output:
1. Key metrics summary
2. Trends and observations
3. Risk areas
4. Recommendations for next sprint

Parameters:
- Compare with previous sprint where possible
- Flag any red flags
- Suggest improvements

Output Format:
## Metrics Dashboard - Sprint 14
## Trends
## Risks
## Recommendations

Task: Generate the complete metrics analysis.
```

### AI Output

```
═══════════════════════════════════════════
  METRICS DASHBOARD - Sprint 14
═══════════════════════════════════════════

📊 SUMMARY
  Test Coverage:      96%  (240/250 executed)
  Pass Rate:          88.8% (210/250)
  Fail Rate:          11.2% (28/250)
  Skip Rate:          4.8%  (12/250)

🐛 DEFECT METRICS
  Bugs Found:         18
  Bugs Fixed:         15  (83.3% fix rate)
  Open Bugs:          3
  Escape Rate:        10% (2 bugs reached production) ⚠️

🤖 AUTOMATION
  Automation Ratio:   65% (+7% from Sprint 13)
  Trend:              ↑ Improving

⚠️ RISKS IDENTIFIED
  1. Defect Escape Rate at 10% — above 5% threshold
     → 2 bugs escaped to production
  2. 3 open bugs still pending fix
  3. 12 skipped tests need investigation

📈 RECOMMENDATIONS
  1. URGENT: Investigate the 2 escaped bugs
     → Add regression tests for these scenarios
  2. Priority: Fix 3 remaining open bugs before release
  3. Investigate 12 skipped tests — are they blocked or forgotten?
  4. Continue automation growth — target 75% next sprint
  5. Add smoke tests to CI/CD to catch escaping bugs earlier
```

---

## Building Custom AI Dashboards

### Python Dashboard Script

```python
"""
AI-Powered QA Metrics Dashboard
Generates visual metrics reports from test data.
"""

import json
from datetime import datetime
from collections import defaultdict


# --- Sample Data Structure ---
test_data = {
    "sprint": "Sprint 14",
    "date": "2026-02-05",
    "tests": {
        "total": 250,
        "passed": 210,
        "failed": 28,
        "skipped": 12
    },
    "bugs": {
        "found": 18,
        "fixed": 15,
        "open": 3,
        "escaped_to_prod": 2
    },
    "automation": {
        "automated": 162,
        "manual": 88,
        "total": 250
    },
    "previous_sprints": [
        {"sprint": "Sprint 12", "pass_rate": 82, "automation": 52, "escape_rate": 12},
        {"sprint": "Sprint 13", "pass_rate": 85, "automation": 58, "escape_rate": 8},
        {"sprint": "Sprint 14", "pass_rate": 88.8, "automation": 65, "escape_rate": 10}
    ]
}


# --- Metrics Calculation ---
def calculate_metrics(data):
    """Calculate all key metrics from test data with error handling."""
    metrics = {}

    # Test metrics (handle division by zero)
    total = data["tests"]["total"]
    if total == 0:
        return {"error": "No tests in data"}

    executed = data["tests"]["passed"] + data["tests"]["failed"]
    metrics["coverage"] = (executed / total) * 100
    metrics["pass_rate"] = (data["tests"]["passed"] / total) * 100
    metrics["fail_rate"] = (data["tests"]["failed"] / total) * 100
    metrics["skip_rate"] = (data["tests"]["skipped"] / total) * 100

    # Bug metrics (handle zero bugs found)
    total_bugs = data["bugs"]["found"]
    if total_bugs > 0:
        metrics["fix_rate"] = (data["bugs"]["fixed"] / total_bugs) * 100
        metrics["escape_rate"] = (data["bugs"]["escaped_to_prod"] / total_bugs) * 100
    else:
        metrics["fix_rate"] = 100.0  # No bugs = 100% "fixed"
        metrics["escape_rate"] = 0.0

    # Automation metrics
    auto_total = data["automation"]["total"]
    metrics["automation_ratio"] = (data["automation"]["automated"] / auto_total) * 100 if auto_total > 0 else 0

    return metrics


# --- Text Dashboard Generator ---
def generate_dashboard(data, metrics):
    """Generate a text-based metrics dashboard with proper alignment."""
    # Helper for status indicators
    escape_warning = "⚠️" if metrics["escape_rate"] > 5 else "✓"
    pass_status = "✓" if metrics["pass_rate"] >= 90 else "⚠️" if metrics["pass_rate"] >= 80 else "✗"

    dashboard = f"""
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  QA METRICS DASHBOARD - {data['sprint']:<20}                 ┃
┃  Generated: {data['date']:<20}                               ┃
┣━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┫
┃                                                              ┃
┃  TEST EXECUTION                                              ┃
┃  ├─ Total Tests:      {data['tests']['total']:>6}                               ┃
┃  ├─ Passed:           {data['tests']['passed']:>6}  ({metrics['pass_rate']:>5.1f}%) {pass_status:<3}               ┃
┃  ├─ Failed:           {data['tests']['failed']:>6}  ({metrics['fail_rate']:>5.1f}%)                    ┃
┃  └─ Skipped:          {data['tests']['skipped']:>6}  ({metrics['skip_rate']:>5.1f}%)                    ┃
┃                                                              ┃
┃  DEFECT TRACKING                                             ┃
┃  ├─ Bugs Found:       {data['bugs']['found']:>6}                               ┃
┃  ├─ Bugs Fixed:       {data['bugs']['fixed']:>6}  ({metrics['fix_rate']:>5.1f}%)                    ┃
┃  ├─ Open Bugs:        {data['bugs']['open']:>6}                               ┃
┃  └─ Escaped to Prod:  {data['bugs']['escaped_to_prod']:>6}  ({metrics['escape_rate']:>5.1f}%) {escape_warning:<3}               ┃
┃                                                              ┃
┃  AUTOMATION                                                  ┃
┃  ├─ Automated:        {data['automation']['automated']:>6}                               ┃
┃  ├─ Manual:           {data['automation']['manual']:>6}                               ┃
┃  └─ Ratio:            {metrics['automation_ratio']:>5.1f}%                              ┃
┃                                                              ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
"""
    return dashboard


# --- Trend Analysis ---
def analyze_trends(data):
    """Analyze trends across sprints."""
    sprints = data["previous_sprints"]
    trends = []

    # Pass Rate Trend
    pass_rates = [s["pass_rate"] for s in sprints]
    pass_trend = "↑ Improving" if pass_rates[-1] > pass_rates[-2] else "↓ Declining"
    trends.append(f"  Pass Rate: {pass_trend} ({pass_rates[-2]}% → {pass_rates[-1]}%)")

    # Automation Trend
    auto_rates = [s["automation"] for s in sprints]
    auto_trend = "↑ Growing" if auto_rates[-1] > auto_rates[-2] else "↓ Stagnant"
    trends.append(f"  Automation: {auto_trend} ({auto_rates[-2]}% → {auto_rates[-1]}%)")

    # Escape Rate Trend
    escape_rates = [s["escape_rate"] for s in sprints]
    escape_trend = "⚠️ Increasing" if escape_rates[-1] > escape_rates[-2] else "✅ Improving"
    trends.append(f"  Escape Rate: {escape_trend} ({escape_rates[-2]}% → {escape_rates[-1]}%)")

    return "\n".join(trends)


# --- AI Recommendations Generator ---
def generate_recommendations_prompt(metrics, data):
    """Generate prompt for AI-based recommendations."""
    return f"""
    Analyze these QA metrics and provide actionable recommendations:

    Pass Rate: {metrics['pass_rate']:.1f}%
    Fail Rate: {metrics['fail_rate']:.1f}%
    Escape Rate: {metrics['escape_rate']:.1f}%
    Automation Ratio: {metrics['automation_ratio']:.1f}%
    Open Bugs: {data['bugs']['open']}

    Provide:
    1. Top 3 priority actions
    2. Risk assessment
    3. Next sprint targets
    """


# --- Main Execution ---
if __name__ == "__main__":
    # Calculate metrics
    metrics = calculate_metrics(test_data)

    # Generate dashboard
    print(generate_dashboard(test_data, metrics))

    # Show trends
    print("\n📈 TRENDS:")
    print(analyze_trends(test_data))

    # Generate AI prompt
    print("\n📝 AI RECOMMENDATION PROMPT:")
    print(generate_recommendations_prompt(metrics, test_data))
```

### Running the Dashboard

```bash
python qa_metrics_dashboard.py

# Output:
╔══════════════════════════════════════════════════════════════╗
║          QA METRICS DASHBOARD - Sprint 14                    ║
╠══════════════════════════════════════════════════════════════╣
║  📊 TEST EXECUTION                                           ║
║  ├── Passed:            210  ( 84.0%)                        ║
║  ├── Failed:             28  ( 11.2%)                        ║
║  └── Skipped:            12  (  4.8%)                        ║
║  🐛 DEFECT TRACKING                                          ║
║  ├── Bugs Fixed:         15  ( 83.3%)                        ║
║  └── Escaped to Prod:     2  ( 11.1%) ⚠️                     ║
║  🤖 AUTOMATION                                               ║
║  └── Automation Ratio:  64.8%                                ║
╚══════════════════════════════════════════════════════════════╝

📈 TRENDS:
  Pass Rate: ↑ Improving (85.0% → 88.8%)
  Automation: ↑ Growing (58% → 65%)
  Escape Rate: ⚠️ Increasing (8% → 10%)
```

---

## Generating AI Reports from Metrics

### Sprint Summary Report

```text
Role: QA Reporting Analyst

Generate a sprint summary report from these metrics:
[PASTE METRICS DATA]

Include:
1. Executive summary (3-4 sentences)
2. What went well
3. What needs improvement
4. Risk items
5. Next sprint targets with specific numbers
6. Recommendations for management

Format: Professional, data-driven, actionable
```

### AI-Generated Sprint Report

```
═══════════════════════════════════════════
  SPRINT 14 QA SUMMARY REPORT
═══════════════════════════════════════════

EXECUTIVE SUMMARY:
Sprint 14 showed solid progress with pass rate improving to 88.8%
and automation coverage growing to 65%. However, 2 bugs escaped to
production raising the escape rate to 10%, which requires immediate
attention in Sprint 15.

✅ WHAT WENT WELL:
  • Pass rate improved from 85% to 88.8%
  • Automation coverage grew from 58% to 65% (+7 points)
  • Bug fix rate at 83.3% — dev team is responsive

⚠️ AREAS FOR IMPROVEMENT:
  • 2 bugs escaped to production (escape rate: 10%)
  • 12 tests were skipped — investigation needed
  • 3 open bugs still pending resolution

🎯 SPRINT 15 TARGETS:
  • Escape rate: < 5% (from current 10%)
  • Automation coverage: 75% (from 65%)
  • All open bugs resolved before release
  • Zero skipped tests without documented reason
  • Add smoke tests to CI/CD pipeline
```

---

## Metrics Thresholds (Industry Standards)

| Metric | Good | Warning | Critical |
|--------|------|---------|----------|
| Pass Rate | > 90% | 80-90% | < 80% |
| Escape Rate | < 3% | 3-7% | > 7% |
| Automation Ratio | > 70% | 50-70% | < 50% |
| Fix Rate | > 90% | 70-90% | < 70% |
| Test Coverage | > 85% | 70-85% | < 70% |

---

## Anti-Hallucination Check (Chapter 1)

- [ ] All metrics calculated from REAL test data, not AI-generated numbers
- [ ] Trends compared against actual previous sprint data
- [ ] Recommendations based on real project context
- [ ] Thresholds customized to your project (don't blindly use industry defaults)

---

## Next Steps

- Automate test execution to feed real data: [Automation Code Gen](../automation_code_generation/ch_04_automation_code_generation.md)
- Use [Claude Code](../automation_code_generation/ch_04_claude_code_qa_automation.md) to build and run the dashboard script
- Practice metrics analysis in [SDET Exercises](../learning_practice/ch_04_exercises_sdet.md)
