
# 🧩 Tools Used in Real Production

| Stage            | Tool                        |
| ---------------- | --------------------------- |
| SCM              | GitHub / GitLab / Bitbucket |
| CI               | Jenkins                     |
| Code Quality     | SonarQube                   |
| SAST             | SonarQube / Checkmarx       |
| Dependency Scan  | OWASP Dependency-Check      |
| Secrets Scan     | Gitleaks                    |
| Container Build  | Docker                      |
| Container Scan   | Trivy                       |
| Artifact Repo    | Nexus / Artifactory         |
| Registry         | AWS ECR                     |
| Orchestration    | Kubernetes                  |
| Runtime Security | Falco                       |
| Monitoring       | Prometheus + Grafana        |

---


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
