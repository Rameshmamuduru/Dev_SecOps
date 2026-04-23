# ☁️ 🔐 IaC SCANNING TOOLS (REAL DEVSECOPS STACK)

---

# 🟢 OPEN SOURCE (MOST USED IN CI/CD)

---

## 🔹 1. Trivy

### Category:

👉 All-in-one IaC + container + SCA scanner

### Why it is used:

✔ Fast CI/CD scanning (Jenkins, GitHub Actions)
✔ Supports Terraform, Kubernetes, Helm, YAML
✔ Easy integration, zero setup complexity

### Command:

```bash id="i1"
trivy config .
```

---

## 🔹 2. Checkov

### Category:

👉 Deep IaC security & compliance scanner

### Why it is used:

✔ Strong Terraform + cloud policy checks
✔ Detects AWS/Azure/GCP misconfigurations
✔ Policy-as-code support (very enterprise-like OSS tool)

### Command:

```bash id="i2"
checkov -d .
```

---

# 🔵 ENTERPRISE TOOLS (REAL PRODUCTION GOVERNANCE)

---

## 🔹 1. Prisma Cloud

### Category:

👉 Cloud security + IaC + CSPM platform

### Why it is used:

✔ Full cloud posture management
✔ Scans IaC before deployment
✔ Detects misconfigurations + runtime risks
✔ Enterprise compliance dashboards

---

## 🔹 2. Snyk

### Category:

👉 Developer-first IaC security platform

### Why it is used:

✔ Terraform + Kubernetes scanning
✔ CI/CD integration (Jenkins, GitHub Actions)
✔ Auto-fix recommendations + PRs
✔ Developer-friendly security feedback

### Command:

```bash id="i3"
snyk iac test
```

---

# 🔁 FINAL COMPARISON (SAME FORMAT YOU WANTED)

| Type           | Tool         | Category                    | Why used                                            |
| -------------- | ------------ | --------------------------- | --------------------------------------------------- |
| 🟢 Open Source | Trivy        | All-in-one scanner          | Fast IaC + container security in CI/CD              |
| 🟢 Open Source | Checkov      | IaC policy scanner          | Deep Terraform + cloud misconfiguration checks      |
| 🔵 Enterprise  | Prisma Cloud | Cloud security platform     | Full IaC + cloud posture + compliance               |
| 🔵 Enterprise  | Snyk         | DevSecOps security platform | Developer-friendly IaC scanning + CI/CD integration |

---

# 🎯 FINAL SIMPLE INTERVIEW ANSWER

> “For IaC scanning, the most widely used open-source tools are Trivy and Checkov, which help detect misconfigurations in Terraform, Kubernetes, and Helm. In enterprise environments, Prisma Cloud and Snyk are commonly used for advanced cloud security posture management, policy enforcement, and CI/CD integration.”

---

# 💡 MEMORY TRICK

```text id="i4"
Open Source → Trivy + Checkov
Enterprise → Prisma Cloud + Snyk
```

---

If you want next, I can give:
👉 “Same table for SCA + Secrets + Image + IaC combined (full DevSecOps cheat sheet)” 🚀
