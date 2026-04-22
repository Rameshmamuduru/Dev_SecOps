# 🐳 1. Scan Dockerfile (before build)

Use a linter to catch issues early.

**Tool:** Hadolint

**When:**

* Pre-commit
* Pull Request (PR)
* CI pipeline (first stage)

**Example (CI step):**

```bash id="d1"
hadolint Dockerfile
```

👉 Stops bad practices **before image is even built**

---

# 🐳 2. Scan Image (during build)

After building the image, scan it for vulnerabilities.

**Tools:**

* Trivy
* Grype

**When:**

* CI pipeline (after build)

**Example:**

```bash id="d2"
docker build -t myapp:latest .
trivy image myapp:latest
```

👉 Finds:

* OS package vulnerabilities
* Library issues

---

# 🐳 3. Scan Image in Registry (continuous)

Once pushed to registry (ECR, Docker Hub, Artifactory):

**Tools:**

* JFrog Xray
* Amazon ECR Image Scanning

**When:**

* Automatically after push
* Continuously when new CVEs appear

👉 Even if image is old, it gets re-evaluated

---

# 🐳 4. Runtime Scanning (real “real-time”)

Scan running containers in Kubernetes/VMs.

**Tools:**

* Wiz
* Falco

**When:**

* After deployment (continuous)

👉 Detects:

* Suspicious activity
* Runtime exploits
* Misconfigurations

---

# 🔁 Full Real-Time Flow (Important)

```text id="flow1"
Dev → Hadolint → Build → Trivy → Push → Xray/ECR Scan → Deploy → Wiz/Falco Monitor
```

---

# ⚡ What “Real-Time” Actually Means

People misunderstand this 👇

| Stage    | Real-Time Meaning          |
| -------- | -------------------------- |
| CI/CD    | Scan on every commit/build |
| Registry | Auto scan when CVEs update |
| Runtime  | Continuous monitoring      |

👉 True real-time = **continuous + automated at all stages**

---

# 🎯 Best Practice (What companies do)

* PR Stage → Hadolint
* Build Stage → Trivy
* Registry → Xray
* Production → Wiz

👉 Multiple layers = strong security
