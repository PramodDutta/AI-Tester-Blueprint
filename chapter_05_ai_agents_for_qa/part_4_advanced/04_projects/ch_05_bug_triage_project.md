# Bug Triage Project

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Project Overview

Automated bug classification, prioritization, and routing agent.

---

## 📋 Features

- Classify bugs by type (UI, API, Security)
- Set priority based on impact
- Check for duplicates
- Route to correct team
- Add appropriate labels

---

## 🛠️ Implementation

```python
from crewai import Agent, Task, Crew

classifier = Agent(
    role="Bug Classifier",
    goal="Classify bugs by type and component",
    llm="claude-3-5-sonnet-20241022"
)

prioritizer = Agent(
    role="Priority Analyst",
    goal="Determine bug priority based on impact",
    llm="claude-3-5-sonnet-20241022"
)

router = Agent(
    role="Bug Router",
    goal="Route bugs to appropriate teams",
    llm="claude-3-5-sonnet-20241022"
)

def triage_bug(bug_report: str):
    classify_task = Task(
        description=f"Classify this bug: {bug_report}",
        agent=classifier
    )
    priority_task = Task(
        description="Determine priority",
        agent=prioritizer,
        context=[classify_task]
    )
    route_task = Task(
        description="Route to team",
        agent=router,
        context=[classify_task, priority_task]
    )
    
    crew = Crew(
        agents=[classifier, prioritizer, router],
        tasks=[classify_task, priority_task, route_task]
    )
    return crew.kickoff()
```

---

## 📊 Example Output

```
Bug: "Users can't checkout on Safari mobile"

Classification:
  Type: UI/Browser Compatibility
  Component: Checkout
  
Priority: P1 (High)
  - Affects revenue
  - Safari mobile is 15% of traffic
  
Routing:
  Team: Frontend
  Labels: [safari, mobile, checkout, p1]
```

---

## 📚 See Also

- [Bug Triage Agents](../../part_1_fundamentals/agent_types_for_qa/ch_05_bug_triage_agents.md)
- [Jira Integration](../integrations/ch_05_jira_integration.md)
