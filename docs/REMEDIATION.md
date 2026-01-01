# Remediation Examples

Before/after comparisons for each violation type.

## Check 04: Hardcoded Secrets

### ❌ Violation (Tazima Fixture)
```python
# app.py
AWS_ACCESS_KEY_ID = "AKIAABCDEFGHIJKLMNOP"
```

### ✅ Remediation
```python
# app.py
import os
AWS_ACCESS_KEY_ID = os.environ.get("AWS_ACCESS_KEY_ID")
```
```bash
# .env (excluded via .gitignore)
AWS_ACCESS_KEY_ID=AKIAABCDEFGHIJKLMNOP
```

### Zimara Detection
```
[CRITICAL] Potential secret pattern detected
  File:    app.py:2
  Pattern: AWS_ACCESS_KEY_ID = "AKIA[A-Z0-9]{16}"
  
  1 | # Fake but pattern-matching AWS key
→ 2 | AWS_ACCESS_KEY_ID = "AKIAABCDEFGHIJKLMNOP"
  3 |

Remediation:
  - Store secrets in environment variables
  - Use secret management (AWS Secrets Manager, Vault)
  - Add .env to .gitignore
  - Rotate exposed credentials immediately
```

[... examples for all check categories ...]
