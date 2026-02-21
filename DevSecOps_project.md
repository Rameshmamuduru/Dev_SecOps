Perfect 👍
I’ll give you a **complete production SonarQube setup from scratch on Ubuntu (AWS EC2)** — clean, secure, industry-standard.

Assumption:

* Ubuntu 22.04
* Fresh EC2
* Public IP
* You want production-ready setup

---

# 🚀 STEP 0 — Create EC2 Properly

Instance:

* Ubuntu 22.04
* Minimum: **t3.medium (4GB RAM required)**
* Security Group:

  * 22 (SSH)
  * 80 (HTTP)
  * 443 (HTTPS)
    ❌ DO NOT open 9000

---

# 🚀 STEP 1 — Update Server

```bash
sudo apt update && sudo apt upgrade -y
```

---

# 🚀 STEP 2 — Install Java (Required)

SonarQube requires Java 17.

```bash
sudo apt install openjdk-17-jdk -y
java -version
```

---

# 🚀 STEP 3 — Install Database

Use:

## 👉 PostgreSQL

```bash
sudo apt install postgresql postgresql-contrib -y
```

Start & enable:

```bash
sudo systemctl enable postgresql
sudo systemctl start postgresql
```

---

## Create Sonar Database

```bash
sudo -u postgres psql
```

Inside psql:

```sql
CREATE DATABASE sonarqube;
CREATE USER sonar WITH ENCRYPTED PASSWORD 'StrongPassword123';
GRANT ALL PRIVILEGES ON DATABASE sonarqube TO sonar;
\q
```

---

# 🚀 STEP 4 — Linux Kernel Tuning (MANDATORY)

Edit:

```bash
sudo nano /etc/sysctl.conf
```

Add:

```
vm.max_map_count=262144
fs.file-max=65536
```

Apply:

```bash
sudo sysctl -p
```

Also:

```bash
sudo nano /etc/security/limits.conf
```

Add:

```
sonar   -   nofile   65536
sonar   -   nproc    4096
```

---

# 🚀 STEP 5 — Create Sonar User

```bash
sudo adduser --system --no-create-home --group --disabled-login sonar
```

---

# 🚀 STEP 6 — Download SonarQube

Go to:

## 👉 SonarQube

```bash
cd /opt
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.4.1.88267.zip
sudo apt install unzip -y
sudo unzip sonarqube-10.4.1.88267.zip
sudo mv sonarqube-10.4.1.88267 sonarqube
```

Permissions:

```bash
sudo chown -R sonar:sonar /opt/sonarqube
```

---

# 🚀 STEP 7 — Configure SonarQube

Edit:

```bash
sudo nano /opt/sonarqube/conf/sonar.properties
```

Uncomment & set:

```
sonar.jdbc.username=sonar
sonar.jdbc.password=StrongPassword123
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube

sonar.web.host=127.0.0.1
sonar.web.port=9000
```

Save.

---

# 🚀 STEP 8 — Create Systemd Service

```bash
sudo nano /etc/systemd/system/sonarqube.service
```

Paste:

```
[Unit]
Description=SonarQube service
After=network.target postgresql.service

[Service]
Type=forking
User=sonar
Group=sonar
ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
LimitNOFILE=65536
LimitNPROC=4096
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable:

```bash
sudo systemctl daemon-reload
sudo systemctl enable sonarqube
sudo systemctl start sonarqube
```

Check:

```bash
sudo systemctl status sonarqube
```

---

# 🚀 STEP 9 — Install Reverse Proxy

Use:

## 👉 Nginx

```bash
sudo apt install nginx -y
```

Create config:

```bash
sudo nano /etc/nginx/sites-available/sonarqube
```

Paste:

```
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:9000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

Enable:

```bash
sudo ln -s /etc/nginx/sites-available/sonarqube /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

Now accessible via:

```
http://your-domain.com
```

---

# 🚀 STEP 10 — Enable HTTPS (Production Required)

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d your-domain.com
```

Now:

```
https://your-domain.com
```

---

# 🔒 FINAL SECURITY

AWS Security Group:

Open only:

* 22
* 80
* 443

Close:

* 9000 ❌

---

# 🎯 Final Production Architecture

```
Internet
   ↓
HTTPS (443)
   ↓
Nginx
   ↓
SonarQube (9000 internal)
   ↓
PostgreSQL
```

---

If you want next level:

* Setup with Docker?
* Setup with Kubernetes?
* Setup behind AWS ALB?
* High availability cluster version?

Tell me your goal (learning / company prod / enterprise).
I’ll design enterprise-grade architecture for you 🚀
