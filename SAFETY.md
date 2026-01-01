# Deployment Safety

Preventing accidental production deployment of Tazima fixtures.

## Repository-Level Protection

### robots.txt
```txt
User-agent: *
Disallow: /

# Tazima: Intentional security violations for testing only
# DO NOT deploy this repository to production
```

### .gitattributes
```
# Prevent secrets scanning false positives
*.key       linguist-generated=true
*.env       linguist-generated=true
*.tf        linguist-generated=true
secret.txt  linguist-generated=true
```

### netlify.toml (if accidentally deployed)
```toml
[build]
  publish = "DEPLOYMENT_BLOCKED"
  command = "echo 'ERROR: Tazima cannot be deployed' && exit 1"

[[headers]]
  for = "/*"
  [headers.values]
    X-Robots-Tag = "noindex, nofollow"
```

## CI/CD Protection

### GitHub Actions - Block Production Deployment
```yaml
name: safety-check
on: [push, pull_request]

jobs:
  prevent-deployment:
    runs-on: ubuntu-latest
    steps:
      - name: Block deployment workflows
        run: |
          if grep -r "deploy" .github/workflows/; then
            echo "ERROR: Deployment workflows detected in test fixture repository"
            exit 1
          fi
```

## Clear Naming Conventions

All generated directories include obvious markers:
- Prefix: `test-violations/`
- Pattern: `check_XX/`
- README files stating "TEST FIXTURE - DO NOT DEPLOY"

## Monitoring

If you accidentally deploy Tazima fixtures:

1. **Immediate rotation**: All "secrets" are fake but rotate real credentials
2. **Remove deployment**: Delete hosted version immediately
3. **Check logs**: Review access logs for reconnaissance attempts
4. **Update .gitignore**: Ensure fixtures never enter production repos
