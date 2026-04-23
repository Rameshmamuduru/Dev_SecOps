# OPEN SOURCE TOOLS (Real DevSecOps Usage)

| Tool              | Category                              | Why it is used in real production                                                                                  |
| ----------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Trivy             | All-in-one scanner (images, SCA, IaC) | Fast CI/CD scanning of Docker images, dependencies, and misconfigurations in pipelines like Jenkins/GitHub Actions |
| Grype (with Syft) | SBOM-based vulnerability scanning     | Generates SBOM (Syft) and performs accurate CVE scanning (Grype); used for deep dependency security validation     |


# ENTERPRISE TOOLS (Production Governance Level)

| Tool       | Category                                   | Why it is used in real production                                                                                            |
| ---------- | ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| JFrog Xray | Artifact security + license compliance     | Scans Docker images and binaries in Artifactory, enforces policies, blocks builds based on vulnerabilities and license rules |
| Snyk       | DevSecOps platform (SCA + container + IaC) | Provides developer-friendly security scanning, automatic fix PRs, CI/CD integration, and full application security coverage  |
