
---

## 📄 2. `.github/workflows/README.md` — for all 3 GitHub Actions workflows

```markdown
# GitHub Workflows for Snyk Security Scans

This folder contains workflows that run Snyk security tests during CI/CD. These workflows help detect and report vulnerabilities in your codebase and dependencies.

---

## 📌 1. `snyk-test-basic.yml`

**Purpose**: Run a Snyk test and upload results as a SARIF file to GitHub's Security tab.

- ✅ Manual trigger or (optional) on push/PR
- 📝 Does **not** fail the build even if vulnerabilities are found
- 📄 Outputs: `snyk-sarif1.json` (uploaded to GitHub code scanning)

---

## 📌 2. `snyk-test-html.yml`

**Purpose**: Run Snyk test on all projects, generate HTML report, and apply filters to fail the build if needed.

- 🛠 Uses `--all-projects` and processes output with `jq`
- 📊 Generates a user-friendly HTML report using `snyk-to-html`
- ❌ Fails the build if filter rules (from `.snyk-filter/snyk.yml`) match
- 📂 Artifacts: `snyk-report.html` downloadable from the Actions tab

---

## 📌 3. `snyk-test-json-only.yml`

**Purpose**: Simpler version of the Snyk test that runs only on the root project.

- ✅ No `jq` processing needed
- 📦 Still supports HTML generation and filtering
- Best for non-monorepo projects or quick scans

---

## 📚 Tools Used

- [Snyk CLI](https://docs.snyk.io/)
- [`snyk-to-html`](https://www.npmjs.com/package/snyk-to-html)
- [`snyk-filter`](https://www.npmjs.com/package/snyk-filter)
- [`jq`](https://stedolan.github.io/jq/) for JSON processing

---

## 🛡️ Recommendations

- Use `snyk-test-html.yml` for full monorepo scans and reporting.
- Use `snyk-test-json-only.yml` for simpler setups.
- Review and update `.snyk-filter/snyk.yml` based on your team's security policy.
