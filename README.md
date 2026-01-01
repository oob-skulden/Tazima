# Zimara Violation Fixture

Intentionally insecure test fixtures used to validate and regression-test  
**Zimara** security checks.

?? **IMPORTANT — READ BEFORE USING**

This repository **intentionally contains insecure patterns**, including:
- Hardcoded secrets (synthetic / non-functional)
- Insecure infrastructure-as-code examples
- Unsafe CI/CD and configuration practices

**These files are NOT vulnerabilities and NOT leaks.**  
They exist solely to exercise detection logic in Zimara.

**DO NOT** copy, reuse, or deploy any files from this repository in real
environments.

---

## Purpose

This repository exists to provide a **deterministic, repeatable test corpus**
for validating Zimara’s security checks.

It is designed to support:
- Validation of new checks before release
- Regression testing across Zimara versions
- Side-by-side comparison of detection results
- CI/CD automation and security tooling demos

In short:  
> If Zimara fails to flag something here, that’s a bug.

---

## Relationship to Zimara

This repository is a **companion test fixture** for the Zimara project.

- Zimara scans code
- This repo **intentionally violates** security best practices
- Together, they enable reliable validation

Zimara repository:  
https://github.com/oob-skulden/zimara

---

## Repository Contents

| Item | Description |
|----|----|
| `zimara_violation_fixtures.sh` | Script that generates intentionally insecure files |
| `fixtures/` | Generated violation files and directories |
| `README.md` | Usage, warnings, and intent |
| `LICENSE` | AGPL-3.0 |

---

## Usage

### 1. Generate the fixtures

```bash
chmod +x zimara_violation_fixtures.sh
./zimara_violation_fixtures.sh
