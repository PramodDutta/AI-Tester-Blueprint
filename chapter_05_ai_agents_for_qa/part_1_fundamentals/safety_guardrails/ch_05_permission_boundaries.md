# Permission Boundaries

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Overview

Define clear boundaries for what agents can and cannot do.

---

## 📋 Permission Matrix

| Resource | Read | Write | Delete |
|----------|------|-------|--------|
| Test files | ✅ | ✅ | ⚠️ Approval |
| Source code | ✅ | ❌ | ❌ |
| Config files | ✅ | ⚠️ | ❌ |
| Test DB | ✅ | ✅ | ✅ |
| Prod DB | ❌ | ❌ | ❌ |
| Jira | ✅ | ⚠️ | ❌ |
| Git | ✅ | ⚠️ PR only | ❌ |

---

## 🔒 Implementation

```python
PERMISSIONS = {
    "file:read": {"scope": ["tests/*", "docs/*"]},
    "file:write": {"scope": ["tests/*"], "requires_approval": False},
    "file:delete": {"scope": ["tests/generated/*"], "requires_approval": True},
    "jira:read": {"all": True},
    "jira:create": {"project": ["QA", "TEST"]},
    "jira:update": {"requires_approval": True},
}

def check_permission(action, resource):
    if not is_allowed(action, resource, PERMISSIONS):
        raise PermissionDenied(f"{action} on {resource}")
```

---

## 📝 Best Practices

1. **Start restrictive** — Open up as needed
2. **Scope narrowly** — Specific paths, not wildcards
3. **Review regularly** — Audit permission usage
4. **Log all access** — For security review

---

## 📚 See Also

- [Sandboxing](ch_05_sandboxing.md)
- [Audit Logging](ch_05_audit_logging.md)
