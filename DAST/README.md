Here are the **most commonly used DAST tools in real production DevSecOps pipelines**, grouped exactly as you asked:

👉 Open Source (Top 2)
👉 Enterprise (Top 2)

Used in real companies with tools like Jenkins

---

# 🌐 🔐 DAST Tools (Dynamic Application Security Testing)

---

# 🆓 1. Open Source DAST Tools (Most Used)

## 🔹 1. OWASP ZAP (MOST POPULAR 🔥)

OWASP ZAP

### Why it’s used:

* Industry standard open-source DAST
* Supports web + API scanning
* CI/CD friendly (Docker, CLI, Jenkins)

### Used for:

✔ SQL Injection
✔ XSS
✔ Authentication issues
✔ API vulnerabilities

👉 This is the **#1 open-source DAST tool in real pipelines**

📌 Evidence: Widely used in CI/CD + DevSecOps pipelines ([OWASP][1])

---

## 🔹 2. Nikto

Nikto

### Why it’s used:

* Fast lightweight scanner
* Server misconfiguration detection

### Used for:

✔ Outdated server software
✔ Dangerous files
✔ Common web misconfigs

---

# 💼 2. Enterprise DAST Tools (Most Used)

## 🔹 1. Burp Suite Enterprise

Burp Suite

### Why companies use it:

* Very powerful crawling engine
* Accurate vulnerability detection
* Enterprise dashboards + reporting

### Used for:

✔ Large-scale web app scanning
✔ CI/CD integration
✔ Compliance reporting

📌 Industry standard in security teams

---

## 🔹 2. Invicti (Acunetix Enterprise)

Invicti

### Why it’s used:

* Very high scan accuracy
* Low false positives
* Fast scanning engine

### Used for:

✔ Enterprise web apps
✔ API security
✔ Continuous scanning

---

# 🔥 Final Summary Table

| Type           | Tool 1                | Tool 2             |
| -------------- | --------------------- | ------------------ |
| 🆓 Open Source | OWASP ZAP             | Nikto              |
| 💼 Enterprise  | Burp Suite Enterprise | Invicti (Acunetix) |

---

# 🚀 Real Production Usage Flow

```text id="z1k9qv"
Code → Build → Deploy to Staging → DAST Scan → Security Gate → Production
```

---
