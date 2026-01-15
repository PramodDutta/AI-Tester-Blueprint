# Local Private LLM Setup using Ollama

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

**Purpose:** Setup guide for running LLMs locally
**Chapter:** 1 - Foundation Model

---

## Why QAs Should Care

| Concern | Why Local LLM Helps |
|---------|---------------------|
| PRDs may be confidential | Data stays on your machine |
| Bug data is sensitive | No cloud transmission |
| Enterprises forbid cloud LLMs | Full compliance |
| Perfect for internal AI test tools | Cost-effective at scale |

---

## What is Ollama?

Ollama is a **local LLM runtime** that lets you run models on your laptop or server.

**Key Benefits:**
- ✅ No clouds
- ✅ No data leakage
- ✅ No API costs
- ✅ Full privacy
- ✅ Works offline

---

## Installation

### Step 1: Download Ollama

**Official Download:**
```
https://ollama.com/download
```

**Available for:**
- macOS
- Windows
- Linux

---

### Step 2: Pull Models

Open your terminal/CMD and run:

```bash
# Mistral - Great for QA tasks
ollama pull mistral

# DeepSeek Coder - For code-related testing
ollama pull deepseek-coder

# Llama 3 - General purpose
ollama pull llama3
```

---

## Running Models

### Interactive Mode

```bash
ollama run mistral
```

Type your prompt and press Enter.

### With a Specific Prompt

```bash
ollama run mistral "Generate test cases for a login feature"
```

---

## Recommended Models for QA

| Model | Best For | Size |
|-------|----------|------|
| **mistral** | Test case generation, PRD analysis | ~4GB |
| **llama3** | General QA tasks, documentation | ~4-8GB |
| **deepseek-coder** | Code review, API testing | ~4GB |
| **codellama** | Test script generation | ~4-7GB |
| **phi** | Quick tasks, lightweight | ~2GB |

---

## System Requirements

### Minimum

- 8GB RAM
- 10GB free disk space
- Modern CPU (Intel/AMD/Apple Silicon)

### Recommended

- 16GB+ RAM
- SSD storage
- GPU (optional, but speeds up inference)

---

## Common Commands

```bash
# List installed models
ollama list

# Pull a model
ollama pull <model-name>

# Remove a model
ollama rm <model-name>

# Show model info
ollama show <model-name>

# Run with custom parameters
ollama run mistral --verbose
```

---

## API Mode (For Integration)

Ollama also provides a REST API:

```bash
# Start API server (runs on port 11434 by default)
ollama serve
```

### Example API Call

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "mistral",
  "prompt": "Generate test cases for user registration"
}'
```

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Model download fails | Check internet connection, retry |
| Out of memory | Use smaller model (phi) or close other apps |
| Slow response | Normal for CPU-only; consider GPU |
| Command not found | Restart terminal after installation |

---

## Security Best Practices

1. **Keep Ollama updated** - Security patches
2. **Don't expose API externally** - Bind to localhost only
3. **Use for internal tools only** - Not production-facing
4. **Audit model outputs** - Apply anti-hallucination rules

---

## See Also

- [PRD to Test Cases with Ollama](ch_01_prd_to_test_cases_ollama.md)
- [LLM Comparisons](../core_concepts/ch_01_llm_comparisons.md)
- [Anti-Hallucination Rules](../rules_checklists/ch_01_anti_hallucination.md)

