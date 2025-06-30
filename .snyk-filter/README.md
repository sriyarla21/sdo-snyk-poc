# Snyk Filter Rules

This folder contains custom rules used by the `snyk-filter` tool to decide whether the CI pipeline should fail based on security issues detected by Snyk.

## 🔍 What the Filter Does

The current filter (`snyk.yml`) is configured to:
- ✅ Check for **high severity vulnerabilities** that are **upgradeable**
- ❌ Fail the build if **any** of these vulnerabilities are found
- 💬 Show a helpful message prompting the developer to review upgrade options

## 📄 Current Filter Config (`version: 2`)

```yaml
version: 2
customFilters:
  filter: ".vulnerabilities |= map(if .isUpgradable == true and .severity == \"high\" then . else empty end)"
  pass: "[.vulnerabilities[] | select(.severity == \"high\" and .isUpgradable == true)] | length"
  msg: "High Severity issues detected. Please review upgrade steps"
