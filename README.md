# Tazima Test Violations

**Companion test suite for [Zimara](https://github.com/oob-skulden/zimara)**  
Published by Oob Skulden™

## ?? Warning

This repository contains **intentional security violations** for testing purposes.

**DO NOT:**
- Deploy these fixtures to production
- Use as boilerplate for real projects
- Commit generated violations to production repositories

**Violations include:**
- Hardcoded secrets and API keys
- Insecure configurations
- Vulnerable dependencies
- Exposed credentials

## Purpose

Tazima validates Zimara's detection capabilities by generating 53 isolated test cases covering all security checks.

Each fixture triggers exactly one Zimara finding (or INFO state for checks that don't produce violations).

## Quick Start

### Generate Test Fixtures
```bash
./tazima.sh ./test-violations
```

### Run Zimara Against Specific Check
```bash
# Download latest Zimara
curl -sSL https://github.com/oob-skulden/zimara/releases/latest/download/zimara.sh -o zimara.sh
chmod +x zimara.sh

# Test against a specific check
./zimara.sh ./test-violations/check_04
```

### Batch Validation
```bash
for d in test-violations/check_*; do
  echo "=== Testing $d ==="
  ./zimara.sh "$d" || true
  echo
done
```

## Coverage

Tazima covers:
- **45 production checks** (Zimara v0.48.0+)
- **8 expansion checks** (Zimara v0.51.0 roadmap)

See [COVERAGE.md](docs/COVERAGE.md) for complete check-by-check mapping.

## Tool Dependencies

Some checks require external tools:
- **CHECK_12**: [gitleaks](https://github.com/gitleaks/gitleaks) (secret scanning)
- **CHECK_13**: [detect-secrets](https://github.com/Yelp/detect-secrets) (secret detection)
- **CHECK_14**: npm (requires network for `npm audit`)

Install these tools before running their respective checks, or they'll be skipped.

## Test Fixture Structure

Each `check_XX` directory contains:
- Minimal git repository
- Single intentional violation
- README.txt explaining expected detection
- Complete isolation from other checks

Example structure:
```
test-violations/
+-- check_03/     # Private key detection
+-- check_04/     # AWS access key pattern
+-- check_19/     # Sensitive filename (id_rsa)
+-- check_46/     # IaC hardcoded secrets
+-- check_47/     # Docker security issues
```

## Integration with CI/CD

See [INTEGRATION.md](docs/INTEGRATION.md) for examples of:
- Pre-commit hook validation
- GitHub Actions workflows
- Regression testing strategies
- Baseline diffing

## Safety Measures

See [SAFETY.md](SAFETY.md) for deployment prevention strategies including:
- Repository-level protection (robots.txt, .gitattributes)
- CI/CD safety checks
- Clear naming conventions
- Monitoring guidance

## Documentation

- **[COVERAGE.md](docs/COVERAGE.md)** - Complete check-by-check matrix with expected outputs
- **[INTEGRATION.md](docs/INTEGRATION.md)** - CI/CD integration examples
- **[REMEDIATION.md](docs/REMEDIATION.md)** - Before/after fix examples for each violation type
- **[SAFETY.md](SAFETY.md)** - Preventing accidental deployment

## Contributing

Found a check that Zimara doesn't detect? Open an issue on the [Zimara repository](https://github.com/oob-skulden/zimara/issues).

Tazima fixtures should always trigger their corresponding Zimara check. If they don't, that's either:
1. A Zimara regression (bug in scanner)
2. A Tazima fixture issue (test case needs updating)

## License

This project is licensed under the **GNU Affero General Public License v3.0**.

See [LICENSE](LICENSE) for the full license text.

Copyright © 2025 Robert G. Walden. Published by Oob Skulden™.

---

**Published by Oob Skulden™**

For the production security scanner, see: **[Zimara](https://github.com/oob-skulden/zimara)**