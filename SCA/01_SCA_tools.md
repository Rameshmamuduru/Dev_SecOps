# 1. OSV Scanner
- Lightweight CLI tool
- Uses OSV database
- Fast scanning in CI

**Best for: quick vulnerability checks**

# 2. OWASP Dependency-Check
- Open-source SCA tool
- Uses NVD (CVE database)
- Can run offline

**Best for: basic SCA in small/medium projects**

# 3. JFrog Xray:
- Enterprise-grade SCA platform
- Scans:
  - dependencies
  - containers
  - binaries
- Provides:
  - continuous monitoring
  - policy enforcement
  - SBOM generation
- Integrates with Artifactory and CI/CD

**It performs end-to-end security across SDLC**

# 4. JFrog Frogbot
- Works with Git (PRs)
- Scans dependencies during pull requests
- Can auto-fix vulnerabilities

**It is not a scanner itself and It uses Xray in the backend**

# 5. GitHub Dependabot:
Github native tool

# 6. Trivy:

| Command        | Purpose                    |
| -------------- | -------------------------- |
| `trivy fs`     | Scan code + dependencies   |
| `trivy image`  | Scan Docker images         |
| `trivy config` | Scan IaC (Terraform, YAML) |



## Table
| Feature               | OSV Scanner | Dependency-Check | Xray | Frogbot      |
| --------------------- | ----------- | ---------------- | ---- | ------------ |
| Vulnerability Scan    | ✅           | ✅                | ✅    | ✅ (via Xray) |
| SCA (full analysis)   | ❌           | ⚠️ Limited       | ✅    | ✅            |
| License Check         | ❌           | ⚠️ Limited       | ✅    | ✅            |
| CI/CD Integration     | ✅           | ✅                | ✅    | ✅            |
| Continuous Monitoring | ❌           | ❌                | ✅    | ✅            |
| Policy Enforcement    | ❌           | ❌                | ✅    | ✅            |
| Auto Fix PR           | ❌           | ❌                | ❌    | ✅            |
| Enterprise Ready      | ❌           | ⚠️               | ✅    | ✅            |


## Real Industry Usage (This is the key insight)
### Small / Learning / Budget Projects
- Use:
  - OSV Scanner
  - Dependency-Check

**Cheap + simple**

- Mid-level Teams
  - Use:
    - Dependency-Check + some automation

- Enterprise / Real Production Systems
- They use combination:
  - Xray → core SCA + monitoring
  - Frogbot → PR-level security + auto-fix
**(Sometimes OSV as additional fast scan)**

**Security is continuous, not one-time scan, Needs policy enforcement + governance**


## Tools Comparision Table:

| Tool                   | What it does                       | Key Capabilities                                                                                                                                | CI/CD Integration                   | Open Source?                                  |
| ---------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- | --------------------------------------------- |
| Trivy                  | Multi-purpose security scanner     | ✔ Dependency (SCA) scanning<br>✔ Container image scanning<br>✔ IaC misconfig scan<br>✔ Secrets detection<br>✔ SBOM generation                   | ✔ Jenkins<br>✔ GitHub Actions       | ✅ Yes                                         |
| OWASP Dependency-Check | Pure SCA tool                      | ✔ Detects CVEs in dependencies<br>✔ Detailed CVSS scoring<br>✔ HTML/JSON reports<br>✔ NVD-based analysis                                        | ✔ Jenkins<br>✔ Maven/Gradle plugins | ✅ Yes                                         |
| GitHub Dependabot      | Dependency monitoring & auto-fix   | ✔ Detects vulnerable dependencies<br>✔ Auto PR updates<br>✔ Version upgrades<br>✔ Alerts in repo                                                | ✔ Native in GitHub (with Actions)   | ⚠️ Partially (service, not fully open source) |
| JFrog Xray             | Enterprise SCA & artifact scanning | ✔ Dependency vulnerability scanning<br>✔ Binary scanning<br>✔ License compliance<br>✔ Policy enforcement<br>✔ Deep integration with Artifactory | ✔ Jenkins<br>✔ GitHub<br>✔ CI tools | ❌ No (Commercial)                             |
| JFrog Frogbot          | Automated PR security scanning     | ✔ Scans dependencies in PRs<br>✔ Comments vulnerabilities<br>✔ Integrates with Xray<br>✔ Shift-left security                                    | ✔ GitHub / GitLab PRs               | ⚠️ Free tool but tied to JFrog ecosystem      |



















