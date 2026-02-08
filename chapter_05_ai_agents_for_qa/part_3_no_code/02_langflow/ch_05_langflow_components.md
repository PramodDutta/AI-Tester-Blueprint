# LangFlow Components

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

LangFlow provides visual components for all LangChain capabilities.

---

## 🧩 Component Categories

### 1. Models

| Component | Purpose |
|-----------|---------|
| **OpenAI** | GPT-4, GPT-3.5 |
| **Anthropic** | Claude models |
| **Ollama** | Local models |
| **Google AI** | Gemini models |

### 2. Prompts

| Component | Purpose |
|-----------|---------|
| **Prompt Template** | Custom instructions |
| **Few-Shot Prompt** | With examples |
| **Chat Prompt** | Multi-turn prompts |

### 3. Agents

| Component | Purpose |
|-----------|---------|
| **Tool Calling Agent** | Use tools |
| **OpenAI Functions** | Function calling |
| **ReAct Agent** | Reason + Act |

### 4. Tools

| Component | Purpose |
|-----------|---------|
| **Search API** | Web search |
| **Calculator** | Math |
| **Python REPL** | Run code |
| **HTTP Request** | API calls |

### 5. Vector Stores (RAG)

| Component | Purpose |
|-----------|---------|
| **Chroma** | Local vector DB |
| **Pinecone** | Cloud vector DB |
| **FAISS** | Fast similarity |

### 6. Document Loaders

| Component | Purpose |
|-----------|---------|
| **File** | Load files |
| **Web** | Load web pages |
| **PDF** | Load PDFs |
| **GitHub** | Load repos |

---

## 📝 Example: QA Knowledge Base

```
┌─────────────────────────────────────────────────────────────────┐
│                  QA KNOWLEDGE BASE FLOW                          │
└─────────────────────────────────────────────────────────────────┘

[File Loader]  →  [Text Splitter]  →  [Embeddings]  →  [Chroma]
   (docs/)           (chunks)           (OpenAI)       (store)
                                            
[Chat Input]  →  [Retriever]  →  [LLM]  →  [Chat Output]
   (query)       (from Chroma)   (Claude)    (answer)
```

---

## 💡 Tips

1. **Start simple** — Chat Input → LLM → Chat Output
2. **Add RAG later** — Vector stores for knowledge
3. **Use Agents** — For complex multi-step tasks
4. **Export code** — Convert flows to Python

---

## 📚 See Also

- [LangFlow Setup](ch_05_langflow_setup.md)
- [Jira RAG Project](ch_05_langflow_jira_rag.md)
