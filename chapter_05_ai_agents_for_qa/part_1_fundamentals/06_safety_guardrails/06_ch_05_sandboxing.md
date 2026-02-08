# Sandboxing

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 What is Sandboxing?

Running agents in isolated environments to prevent unintended damage.

---

## 🛡️ Sandboxing Strategies

### 1. Container Isolation
```dockerfile
# Run agent in Docker container
FROM python:3.11
RUN pip install agent-framework
# Limited network, no host access
```

### 2. Virtual Environment
```bash
# Separate Python environment
python -m venv agent_sandbox
source agent_sandbox/bin/activate
```

### 3. Database Isolation
```
Production DB ←── READ ONLY ── Agent
Test DB      ←── FULL ACCESS ── Agent
```

### 4. Network Restrictions
```yaml
# Allow only specific domains
allowed_domains:
  - api.jira.com
  - api.slack.com
  - staging.myapp.com
blocked:
  - production.myapp.com
```

---

## 📋 Sandbox Checklist

- [ ] Agent runs in container/VM
- [ ] No access to production systems
- [ ] Network restricted to allowed hosts
- [ ] File system access limited
- [ ] Credentials use test accounts
- [ ] Actions are reversible

---

## 📚 See Also

- [Safety Fundamentals](ch_05_safety_fundamentals.md)
- [Permission Boundaries](ch_05_permission_boundaries.md)
