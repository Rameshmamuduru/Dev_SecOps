| #  | Use Case                         | Command                                                                                       | Where used in pipeline     |
| -- | -------------------------------- | --------------------------------------------------------------------------------------------- | -------------------------- |
| 1  | Baseline scan (MOST USED)        | `zap-baseline.py -t http://staging-app -r report.html`                                        | CI builds / PR validation  |
| 2  | Full active scan (deep scan)     | `zap-full-scan.py -t http://staging-app -r report.html`                                       | Nightly / pre-prod         |
| 3  | API scan (Swagger/OpenAPI)       | `zap-api-scan.py -t http://staging-app/swagger.json -f openapi -r api.html`                   | Microservices / APIs       |
| 4  | Quick CLI scan                   | `zap.sh -cmd -quickurl http://staging-app -quickout report.html`                              | Simple CI checks           |
| 5  | JSON output (automation parsing) | `zap-baseline.py -t http://staging-app -J report.json`                                        | Jenkins parsing / gates    |
| 6  | Docker-based baseline scan       | `docker run -t owasp/zap2docker-stable zap-baseline.py -t http://staging-app -r report.html`  | Cloud CI/CD pipelines      |
| 7  | Docker full scan                 | `docker run -t owasp/zap2docker-stable zap-full-scan.py -t http://staging-app -r report.html` | Pre-production security    |
| 8  | Authenticated scan               | `zap-baseline.py -t http://staging-app -r report.html -z "-config api.key=123456"`            | Login-based apps           |
| 9  | Fail pipeline on HIGH risk       | `grep -i "High" report.html && exit 1`                                                        | Security gate in Jenkins   |
| 10 | Parallel scan execution          | `parallel { zap-baseline.py ... }`                                                            | Large enterprise pipelines |
| 11 | Silent mode execution            | `zap.sh -daemon -port 8080`                                                                   | Background scanning        |
| 12 | Stop ZAP session (cleanup)       | `zap-cli shutdown`                                                                            | Post pipeline cleanup      |
