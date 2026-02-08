# LangChain Agents for QA

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

LangChain is the most popular framework for building LLM applications and agents.

---

## 📦 Installation

```bash
pip install langchain langchain-anthropic langchain-openai
```

---

## 🛠️ Basic QA Agent

```python
from langchain.agents import AgentExecutor, create_react_agent
from langchain_anthropic import ChatAnthropic
from langchain.tools import Tool
from langchain import hub

# Initialize LLM
llm = ChatAnthropic(
    model="claude-3-5-sonnet-20241022",
    temperature=0
)

# Define QA tools
def run_playwright_tests(test_file: str) -> str:
    """Run Playwright tests and return results."""
    import subprocess
    result = subprocess.run(
        ["npx", "playwright", "test", test_file],
        capture_output=True,
        text=True
    )
    return result.stdout + result.stderr

def create_jira_bug(title: str, description: str) -> str:
    """Create a bug in Jira."""
    # Jira API integration here
    return f"Created: BUG-{hash(title) % 10000}"

def read_test_file(file_path: str) -> str:
    """Read a test file."""
    with open(file_path, 'r') as f:
        return f.read()

tools = [
    Tool(
        name="run_tests",
        func=run_playwright_tests,
        description="Run Playwright tests. Input: test file path"
    ),
    Tool(
        name="create_bug",
        func=create_jira_bug,
        description="Create a Jira bug. Input: 'title|description'"
    ),
    Tool(
        name="read_file",
        func=read_test_file,
        description="Read a test file. Input: file path"
    ),
]

# Get ReAct prompt
prompt = hub.pull("hwchase17/react")

# Create agent
agent = create_react_agent(llm, tools, prompt)
agent_executor = AgentExecutor(
    agent=agent,
    tools=tools,
    verbose=True,
    max_iterations=10
)

# Run agent
result = agent_executor.invoke({
    "input": "Run the login tests and create a bug if any fail"
})
print(result["output"])
```

---

## 🔧 Agent with Memory

```python
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory(
    memory_key="chat_history",
    return_messages=True
)

agent_executor = AgentExecutor(
    agent=agent,
    tools=tools,
    memory=memory,
    verbose=True
)

# Agent now remembers conversation
agent_executor.invoke({"input": "Run login tests"})
agent_executor.invoke({"input": "What were the results?"})  # Remembers!
```

---

## 📊 Structured Outputs

```python
from langchain.output_parsers import PydanticOutputParser
from pydantic import BaseModel
from typing import List

class TestCase(BaseModel):
    id: str
    title: str
    steps: List[str]
    expected: str
    priority: str

parser = PydanticOutputParser(pydantic_object=TestCase)

prompt = f"""
Generate a test case for login functionality.
{parser.get_format_instructions()}
"""

response = llm.invoke(prompt)
test_case = parser.parse(response.content)
```

---

## 📚 See Also

- [Frameworks Overview](ch_05_frameworks_overview.md)
- [CrewAI Teams](ch_05_crewai_teams.md)
