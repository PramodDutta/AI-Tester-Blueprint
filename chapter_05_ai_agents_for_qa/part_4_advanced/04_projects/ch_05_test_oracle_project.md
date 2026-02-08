# Test Oracle Project

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Project Overview

Build an AI agent that answers QA team questions using your test documentation and historical data.

---

## 📋 Features

- Answer questions about test coverage
- Explain why tests fail
- Suggest test improvements
- Query historical test results

---

## 🛠️ Implementation

```python
from langchain.agents import AgentExecutor, create_react_agent
from langchain_anthropic import ChatAnthropic
from langchain.vectorstores import Chroma
from langchain.embeddings import OpenAIEmbeddings
from langchain.tools import Tool

# Set up RAG
embeddings = OpenAIEmbeddings()
vectorstore = Chroma(
    persist_directory="./test_knowledge",
    embedding_function=embeddings
)

def query_knowledge(question: str) -> str:
    """Query the QA knowledge base."""
    docs = vectorstore.similarity_search(question, k=3)
    return "\n".join([d.page_content for d in docs])

def get_test_history(test_name: str) -> str:
    """Get historical results for a test."""
    # Query your test results database
    return f"Last 10 runs: 8 passed, 2 failed"

def analyze_failure(error_log: str) -> str:
    """Analyze test failure."""
    llm = ChatAnthropic(model="claude-3-5-sonnet-20241022")
    return llm.invoke(f"Analyze this test failure: {error_log}").content

# Create agent
tools = [
    Tool(name="search_docs", func=query_knowledge, description="Search QA docs"),
    Tool(name="test_history", func=get_test_history, description="Get test history"),
    Tool(name="analyze_failure", func=analyze_failure, description="Analyze failures"),
]

llm = ChatAnthropic(model="claude-3-5-sonnet-20241022")
# ... create agent with tools
```

---

## 💬 Example Queries

- "Why does the login test keep failing on Fridays?"
- "What's our test coverage for the payment module?"
- "Show me similar bugs to BUG-123"
- "What tests should I run for a change to auth.py?"

---

## 📚 See Also

- [RAG for QA](../advanced_topics/ch_05_rag_for_qa.md)
- [Bug Triage Project](ch_05_bug_triage_project.md)
