# Tazima Coverage Matrix

This document maps each Tazima fixture to its corresponding Zimara check.

## Repository Hygiene (Checks 01-02)

| Check | Severity | Violation | Expected Output |
|-------|----------|-----------|-----------------|
| 01 | FAIL | Missing `.git` directory | "No .git directory found" |
| 02 | WARN | Missing `.gitignore` | "Missing .gitignore" |

## Secret Detection (Checks 03-04, 12-13)

| Check | Severity | Violation | Expected Output |
|-------|----------|-----------|-----------------|
| 03 | CRITICAL | Private key in file | "Private key found: leaked.key:1" |
| 04 | CRITICAL | AWS access key pattern | "Secret pattern found: app.py:2" |
| 12 | CRITICAL | GitHub token (gitleaks) | Tool-dependent output |
| 13 | CRITICAL | API key (detect-secrets) | Tool-dependent output |

[... continue for all 53 checks ...]

## Usage Example
```bash
# Test secret detection
./zimara.sh ./test-violations/check_04 --format json

# Expected JSON output:
{
  "findings": [{
    "check_id": "04",
    "severity": "CRITICAL",
    "file": "app.py",
    "line": 2,
    "message": "Potential secret pattern detected",
    "pattern": "AWS_ACCESS_KEY_ID"
  }]
}
```
