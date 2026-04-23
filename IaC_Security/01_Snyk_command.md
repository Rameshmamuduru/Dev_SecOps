| 🧾 Command                                | 🎯 Purpose / Use                                                                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------- |
| `snyk auth`                               | Authenticate CLI with Snyk account (opens browser login)                              |
| `snyk iac test`                           | Scan current directory for IaC security issues (Terraform, K8s, Helm, CloudFormation) |
| `snyk iac test ./terraform`               | Scan only Terraform files in a specific folder                                        |
| `snyk iac test ./k8s`                     | Scan Kubernetes YAML files in a directory                                             |
| `snyk iac test --severity-threshold=high` | Fail pipeline if HIGH or CRITICAL IaC issues are found                                |
| `snyk iac test --json > report.json`      | Generate machine-readable JSON report for CI/CD pipelines                             |
| `snyk iac test --sarif > report.sarif`    | Generate SARIF report for GitHub Security tab integration                             |
| `snyk monitor`                            | Upload snapshot of project to Snyk dashboard for continuous monitoring                |
| `snyk iac test --policy-path=.snyk`       | Apply custom security policies during scanning                                        |
| `snyk ignore`                             | Ignore specific detected issues (used for exceptions)                                 |
| `snyk iac --help`                         | Show all available IaC commands and options                                           |
