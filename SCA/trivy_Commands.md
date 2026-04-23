Got it — you want **real-time, production-ready Trivy commands** (not just basic ones).
Here are the **actual commands used in CI/CD pipelines** with Trivy 👇

---

# 🚀 🔥 1. Code + Dependency Scan (SCA)

```bash
trivy fs . \
  --scanners vuln \
  --severity HIGH,CRITICAL \
  --ignore-unfixed \
  --exit-code 1
```

✔ Scans dependencies
✔ Fails build on HIGH/CRITICAL
✔ Ignores unfixed CVEs

---

# 🔐 🔥 2. Secrets Scan (important)

```bash
trivy fs . \
  --scanners secret \
  --exit-code 1
```

✔ Detects API keys, passwords
✔ Fails if secrets found

---

# 📜 🔥 3. License Scan

```bash
trivy fs . \
  --scanners license \
  --severity HIGH,CRITICAL \
  --exit-code 1
```

✔ Detects risky licenses (GPL, etc.)

---

# ⚙️ 🔥 4. Dockerfile / IaC Scan

```bash
trivy config . \
  --severity HIGH,CRITICAL \
  --exit-code 1
```

✔ Finds:

* Running as root
* Insecure configs

---

# 🐳 🔥 5. Docker Image Scan (MOST IMPORTANT)

```bash
trivy image my-app:1.0 \
  --severity HIGH,CRITICAL \
  --ignore-unfixed \
  --exit-code 1
```

✔ Scans:

* Base image
* OS packages
* App dependencies

---

# 📊 🔥 6. Generate Reports (for audit)

---

## JSON report

```bash
trivy image my-app:1.0 -f json -o report.json
```

---

## HTML report

```bash
trivy image my-app:1.0 -f table -o report.txt
```

---

## SARIF (for GitHub Security)

```bash
trivy fs . -f sarif -o report.sarif
```

---

# ⚡ 🔥 7. Fast Mode (for pipelines)

```bash
trivy image my-app:1.0 \
  --severity HIGH,CRITICAL \
  --timeout 5m \
  --exit-code 1
```

---

# 🔁 🔥 Real Pipeline Commands (Most Used Combo)

👉 This is what most companies run:

```bash
trivy fs . --severity HIGH,CRITICAL --exit-code 1
trivy config . --severity HIGH,CRITICAL --exit-code 1
trivy image my-app:1.0 --severity HIGH,CRITICAL --exit-code 1
```

---

# 🧠 🔥 What each command covers

| Command        | Purpose                   |
| -------------- | ------------------------- |
| `trivy fs`     | Dependencies (SCA)        |
| `trivy config` | Dockerfile / IaC          |
| `trivy image`  | Container vulnerabilities |

---
