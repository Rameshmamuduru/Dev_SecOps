| Stage                      | Open-Source Tool                                            | Enterprise Tool                                                                                 |
| -------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Source Code / SAST**     | SonarQube Community, PMD, SpotBugs, ESLint, Bandit          | SonarQube Enterprise, Checkmarx, Veracode, Fortify, CAST Highlight                              |
| **Dependency / OSS Scan**  | Trivy FS, Snyk CLI, OWASP Dependency-Check, Retire.js       | Snyk Enterprise, WhiteSource/Mend, Black Duck, FOSSA, JFrog Xray                                |
| **Docker Image Scan**      | Trivy image, Clair, Anchore OSS                             | Aqua Security, Anchore Enterprise, JFrog Xray, Twistlock (Prisma Cloud), Snyk Container, Qualys |
| **Kubernetes / Helm Scan** | kubeval, kube-score, conftest, Polaris, KICS                | Datree, Prisma Cloud (Twistlock), Aqua Security, Sysdig Secure, Fugue                           |
| **Secrets Detection**      | GitLeaks, TruffleHog, Detect Secrets                        | Snyk Secrets, Aqua Security, Vault Enterprise, Checkmarx                                        |
| **Infrastructure as Code** | Terraform Validate, TFLint, Checkov                         | Checkov Enterprise, Prisma Cloud, Bridgecrew Enterprise                                         |
| **CI/CD Security**         | Jenkinsfile Linter, GitHub Actions Security Scans, OpenSCAP | GitLab Ultimate, Jenkins X Enterprise, XebiaLabs XL Deploy, GitHub Enterprise Security          |
| **Container Runtime**      | Falco, kube-bench                                           | Twistlock / Prisma Cloud, Aqua Runtime, Sysdig Secure                                           |
| **Cloud Security**         | ScoutSuite, Prowler, Cloud Custodian                        | Prisma Cloud, Dome9, Check Point CloudGuard, Tenable.io                                         |
| **Policy as Code**         | OPA (Open Policy Agent), Conftest                           | OPA Enterprise, Styra, Datree, Chef InSpec                                                      |


## DAST Tools:
| Tool               | Type                     | Usage                 |
| ------------------ | ------------------------ | --------------------- |
| Burp Suite         | Manual + Enterprise DAST | Deep security testing |
| OWASP ZAP          | CI/CD DAST               | Automation pipelines  |
| Acunetix           | Enterprise DAST          | Fast scanning         |
| Netsparker/Invicti | Enterprise DAST          | Compliance-heavy orgs |
| Veracode           | Full AppSec platform     | Governance            |
| Checkmarx          | SAST + DAST              | Unified security      |
| Rapid7 AppSec      | Cloud DAST               | SaaS apps             |
