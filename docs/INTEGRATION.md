# CI/CD Integration

## Pre-Commit Hook Validation
```bash
#!/usr/bin/env bash
# .git/hooks/pre-commit

# Generate fresh fixtures
./tazima.sh /tmp/zimara-test

# Run Zimara self-test
for check in /tmp/zimara-test/check_{03,04,19,46}; do
  if ! ./zimara.sh "$check" --quiet; then
    echo "Zimara failed self-test on $check"
    exit 1
  fi
done

echo "Zimara validation: PASS"
```

## GitHub Actions - Continuous Validation
```yaml
name: zimara-self-test
on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Generate fixtures
        run: ./tazima.sh ./violations
      
      - name: Run Zimara against fixtures
        run: |
          ./zimara.sh ./violations/check_04 --format json > results.json
          
      - name: Verify detection
        run: |
          if ! jq -e '.findings | length > 0' results.json; then
            echo "ERROR: Zimara failed to detect violations"
            exit 1
          fi
```

## Regression Testing
```bash
# Baseline current behavior
./zimara.sh ./violations/check_04 --format json --output baseline.json

# After Zimara changes, compare
./zimara.sh ./violations/check_04 --format json --output current.json
diff baseline.json current.json
```
