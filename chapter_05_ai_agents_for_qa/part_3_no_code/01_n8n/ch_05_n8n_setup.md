# n8n Setup

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is n8n?

n8n is a workflow automation platform with powerful AI capabilities. Think of it as Zapier with AI agents built-in.

---

## 📦 Installation Options

### Option 1: Docker (Recommended)

```bash
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v n8n_data:/home/node/.n8n \
  n8nio/n8n
```

Access at: http://localhost:5678

### Option 2: npm

```bash
npm install n8n -g
n8n start
```

### Option 3: n8n Cloud

Sign up at https://n8n.cloud for hosted version.

---

## 🔧 Initial Configuration

### 1. Create Account
- Open http://localhost:5678
- Create admin account
- Set up 2FA (recommended)

### 2. Configure AI Credentials

**OpenAI:**
1. Settings → Credentials → Add Credential
2. Select "OpenAI"
3. Enter API key

**Claude (Anthropic):**
1. Settings → Credentials → Add Credential
2. Select "Anthropic"
3. Enter API key

---

## 🧪 Quick Test: Hello World Workflow

1. Click **Add workflow**
2. Add **Manual Trigger** node
3. Add **AI Agent** node
4. Connect them
5. Configure AI Agent with your OpenAI/Anthropic key
6. Add system prompt: "You are a helpful QA assistant"
7. Click **Test workflow**
8. Send: "Hello, what can you help with?"

---

## 💡 Key Features for QA

| Feature | Use Case |
|---------|----------|
| **HTTP Request** | Call APIs, webhooks |
| **AI Agent** | Intelligent processing |
| **Jira** | Bug management |
| **GitHub** | Code integration |
| **Slack** | Notifications |
| **Schedule** | Periodic tests |

---

## 📚 See Also

- [n8n AI Nodes](ch_05_n8n_ai_nodes.md)
- [Test Plan Generator](ch_05_n8n_test_plan_generator.md)
