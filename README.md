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

Tazima validates Zimara's detection capabilities by generating
53 isolated test cases covering all security checks.

Each fixture triggers exactly one Zimara finding (or INFO state
for checks that don't produce violations).

## Quick Start

### Generate Test Fixtures
```bash