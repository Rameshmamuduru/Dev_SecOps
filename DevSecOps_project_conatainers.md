Good 🔥 now we are moving to **real production mindset**.

You want:

> How to achieve production SonarQube setup using containers?

We will build proper architecture using:

* SonarQube
* PostgreSQL
* Docker
* Nginx

---

# 🎯 Production Container Architecture

```
Internet
   ↓
Nginx (Reverse Proxy + SSL)
   ↓
SonarQube Container
   ↓
PostgreSQL Container
   ↓
Docker Volume (Persistent Storage)
```

We DO NOT expose port 9000 publicly.

---

# 🚀 STEP 1 — Install Docker

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker
sudo systemctl start docker
```

---

# 🚀 STEP 2 — Kernel Tuning (MANDATORY even in containers)

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

---

# 🚀 STEP 3 — Create Project Directory

```bash
mkdir sonarqube-prod
cd sonarqube-prod
```

---

# 🚀 STEP 4 — Create docker-compose.yml

```bash
nano docker-compose.yml
```

Paste:

```yaml
version: "3.8"

services:

  db:
    image: postgres:15
    container_name: sonarqube-db
    restart: always
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: StrongPassword123
      POSTGRES_DB: sonarqube
    volumes:
      - postgresql_data:/var/lib/postgresql/data

  sonarqube:
    image: sonarqube:community
    container_name: sonarqube
    restart: always
    depends_on:
      - db
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonarqube
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: StrongPassword123
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_logs:/opt/sonarqube/logs
    ports:
      - "127.0.0.1:9000:9000"

volumes:
  postgresql_data:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
```

---

# 🚀 STEP 5 — Start Containers

```bash
docker compose up -d
```

Check:

```bash
docker ps
```

Test internally:

```bash
curl http://localhost:9000
```

---

# 🚀 STEP 6 — Add Nginx Reverse Proxy

Install:

```bash
sudo apt install nginx -y
```

Create config:

```bash
sudo nano /etc/nginx/sites-available/sonarqube
```

Paste:

```nginx
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

# 🚀 STEP 7 — Enable HTTPS

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d your-domain.com
```

Now:

```
https://your-domain.com
```

---

# 🔒 Production Security Checklist

✅ Port 9000 NOT open in AWS
✅ Only 80 and 443 open
✅ DB not exposed
✅ Persistent volumes used
✅ HTTPS enabled

---

# 🎯 Why This Is Production Grade

* Containers isolate services
* DB persistent
* Sonar persistent
* Reverse proxy secure
* Can scale horizontally later
* Easy backup (docker volume backup)

---

# 🚀 If You Want Next Level

We can do:

* Docker Swarm cluster
* Kubernetes deployment
* AWS ALB + ECS
* EKS production setup
* High Availability SonarQube (Enterprise edition)

---

Tell me:

Are you preparing for:

* DevOps job?
* Real company production?
* Learning containers deeply?

I’ll take you to next level accordingly 💪
