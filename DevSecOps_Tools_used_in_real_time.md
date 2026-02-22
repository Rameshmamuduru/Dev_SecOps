| Stage                      | Purpose                    | Open Source Tools       | Enterprise / SaaS Tools      |
| -------------------------- | -------------------------- | ----------------------- | ---------------------------- |
| **SCM**                    | Source Control             | Git                     | GitHub, GitLab, Bitbucket    |
| **Pre-Commit Hooks**       | Prevent bad commits        | pre-commit, Husky       | GitHub Advanced Security     |
| **CI**                     | Build automation           | Jenkins                 | GitHub Actions, GitLab CI    |
| **Code Quality**           | Code smells & bugs         | SonarQube Community     | SonarQube Enterprise         |
| **SAST**                   | Static code security       | SonarQube               | Checkmarx, Veracode, Fortify |
| **Dependency Scan (SCA)**  | Library vulnerabilities    | OWASP Dependency-Check  | Snyk, Black Duck, Mend       |
| **Secrets Scan**           | Hardcoded secrets          | Gitleaks, TruffleHog    | GitGuardian                  |
| **License Compliance**     | OSS license risks          | OWASP DC                | FOSSA, Black Duck            |
| **Build Tool**             | Package build              | Maven, Gradle, npm      | —                            |
| **Container Build**        | Image creation             | Docker                  | BuildKit                     |
| **Container Image Scan**   | Scan image CVEs            | Trivy, Grype            | Prisma Cloud, Aqua           |
| **SBOM Generation**        | Software Bill of Materials | Syft, Trivy             | Anchore Enterprise           |
| **Artifact Repository**    | Store artifacts            | Nexus OSS               | Nexus Pro, Artifactory       |
| **Container Registry**     | Store images               | Harbor                  | AWS ECR                      |
| **IaC Scan**               | Terraform/Helm security    | Checkov, tfsec          | Prisma Cloud                 |
| **Kubernetes Config Scan** | Cluster config security    | kube-bench, kube-hunter | Aqua, Sysdig Secure          |
| **Policy Enforcement**     | Admission control          | OPA Gatekeeper, Kyverno | —                            |
| **DAST**                   | Runtime app testing        | OWASP ZAP               | Burp Suite, Invicti          |
| **Orchestration**          | Container management       | Kubernetes              | OpenShift                    |
| **Runtime Security**       | Detect live attacks        | Falco                   | Aqua, Sysdig                 |
| **Cloud Security (CSPM)**  | AWS/Azure misconfig scan   | Prowler                 | AWS Security Hub             |
| **Secrets Management**     | Central secret storage     | HashiCorp Vault         | AWS Secrets Manager          |
| **Monitoring**             | Metrics                    | Prometheus              | Datadog                      |
| **Visualization**          | Dashboards                 | Grafana                 | Grafana Cloud                |
| **Log Management**         | Log analysis               | ELK Stack               | Splunk                       |
| **Incident Response**      | Alerting                   | Alertmanager            | PagerDuty                    |


# 📦 Sample Enterprise Jenkinsfile (Realistic)

```groovy
pipeline {
    agent any

    tools {
        maven 'MAVEN'
        jdk 'JDK17'
    }

    environment {
        IMAGE_NAME = "devsecops-app"
        REGISTRY = "xxxx.dkr.ecr.ap-south-1.amazonaws.com"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SONARQUBE_SERVER') {
                    sh 'mvn clean verify sonar:sonar'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Dependency Scan') {
            steps {
                sh 'dependency-check.sh --scan .'
            }
        }

        stage('Build Artifact') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$BUILD_NUMBER .'
            }
        }

        stage('Container Scan') {
            steps {
                sh 'trivy image --exit-code 1 --severity HIGH,CRITICAL $IMAGE_NAME:$BUILD_NUMBER'
            }
        }

        stage('Push to Registry') {
            steps {
                sh '''
                aws ecr get-login-password --region ap-south-1 | \
                docker login --username AWS --password-stdin $REGISTRY
                docker tag $IMAGE_NAME:$BUILD_NUMBER $REGISTRY/$IMAGE_NAME:$BUILD_NUMBER
                docker push $REGISTRY/$IMAGE_NAME:$BUILD_NUMBER
                '''
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh '''
                kubectl set image deployment/myapp \
                myapp=$REGISTRY/$IMAGE_NAME:$BUILD_NUMBER
                '''
            }
        }
    }
}
```

---

| Project Type            | Tool Used    |
| ----------------------- | ------------ |
| Java                    | Maven plugin |
| NodeJS                  | CLI          |
| Python                  | CLI          |
| .NET                    | CLI          |
| Container               | Trivy        |
| Multi-language monorepo | CLI          |



# Git Leaks:
```
wget https://github.com/gitleaks/gitleaks/releases/download/v8.30.0/gitleaks_8.30.0_darwin_x64.tar.gz
tar -xvzf gitleaks_linux_x64.tar.gz
sudo mv gitleaks /usr/local/bin/
```
Run scan local
```
gitleaks detect --source . --report-path gitleaks-report.json
```

```
stage('Secret Scan') {
    steps {
        sh '''
        gitleaks detect \
        --source . \
        --report-format json \
        --report-path gitleaks-report.json
        '''
    }
}
```

