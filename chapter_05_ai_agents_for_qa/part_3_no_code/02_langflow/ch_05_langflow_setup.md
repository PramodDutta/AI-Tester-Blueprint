# LangFlow Setup

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is LangFlow?

LangFlow is a visual UI for building LangChain applications. Drag-and-drop LLM pipelines without code.

---

## 📦 Installation

### Option 1: pip (Recommended)

```bash
pip install langflow
langflow run
```

Access at: http://localhost:7860

### Option 2: Docker

```bash
docker run -d -p 7860:7860 langflowai/langflow
```

### Option 3: Astra Langflow (Cloud)

Sign up at https://astra.datastax.com/langflow

---

## 🔧 Initial Configuration

### 1. Open LangFlow

Navigate to http://localhost:7860

### 2. Add API Keys

1. Click **Settings** (gear icon)
2. Add OpenAI API Key
3. Add Anthropic API Key (optional)

### 3. Create First Flow

1. Click **New Project**
2. Name it "QA Assistant"
3. You'll see the flow canvas

---

## 🧪 Quick Test: Simple Chat

1. Drag **Chat Input** component
2. Drag **OpenAI** or **Anthropic** LLM
3. Drag **Chat Output** component
4. Connect: Input → LLM → Output
5. Click **Playground** to test

---

## 💡 Key Components for QA

| Component | Purpose |
|-----------|---------|
| **Chat Input** | Receive user queries |
| **LLM** | AI processing |
| **Prompt** | Custom instructions |
| **Document Loader** | Load test docs |
| **Vector Store** | RAG storage |
| **Agent** | Autonomous actions |

---

## 📚 See Also

- [LangFlow Components](ch_05_langflow_components.md)
- [Jira RAG Project](ch_05_langflow_jira_rag.md)
