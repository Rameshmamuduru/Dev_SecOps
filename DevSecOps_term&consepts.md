# 🔎 What is SAST?

## 🛠 SAST = Static Application Security Testing

SAST analyzes **source code, bytecode, or binaries**
👉 Without running the application.

Think of it as:

> "Reading the code and finding security mistakes"

---

## 🧠 How SAST Works

* Scans source code
* Uses predefined security rules
* Detects patterns like:

  * SQL injection
  * Hardcoded passwords
  * Insecure API usage
  * XSS risks
  * Buffer overflow

---

## 📍 When It Runs?

In CI pipeline:

```text
Git Push → Build → SAST Scan → Continue or Fail
```

---

## 🧪 Popular SAST Tools

* SonarQube
* Checkmarx
* Fortify
* Semgrep

---

## ✅ Advantages of SAST

✔ Finds issues early
✔ Shift-left security
✔ Works before deployment
✔ Helps developers fix quickly

---

## ❌ Limitations

❌ Can produce false positives
❌ Doesn’t detect runtime issues
❌ Cannot detect misconfigurations easily

---

# 🌐 What is DAST?

## 🛠 DAST = Dynamic Application Security Testing

DAST tests a **running application**.

Think of it as:

> "Hacking your app from outside like an attacker"

---

## 🧠 How DAST Works

* Sends malicious inputs
* Tries SQL injection
* Tries XSS payloads
* Tries auth bypass
* Analyzes HTTP responses

It does NOT see the source code.

---

## 📍 When It Runs?

After deployment to staging:

```text
Deploy → DAST Scan → Report vulnerabilities
```

---

## 🧪 Popular DAST Tools

* OWASP ZAP
* Burp Suite
* Netsparker

---

## ✅ Advantages of DAST

✔ Finds runtime issues
✔ Detects real exploitable vulnerabilities
✔ Simulates attacker behavior
✔ No source code needed

---

## ❌ Limitations

❌ Slower
❌ Needs deployed app
❌ Harder to pinpoint exact line of code

---

# 📊 SAST vs DAST Comparison

| Feature       | SAST          | DAST                    |
| ------------- | ------------- | ----------------------- |
| Code required | Yes           | No                      |
| Runs when     | Before deploy | After deploy            |
| Access type   | White-box     | Black-box               |
| Finds         | Coding issues | Runtime vulnerabilities |
| Speed         | Faster        | Slower                  |

---


# 🚀 Advanced Concept: IAST & RASP

For deeper security maturity:

### IAST (Interactive Application Security Testing)

* Combines SAST + DAST
* Runs inside app during testing

Example:

* Contrast Security

---

### RASP (Runtime Application Self-Protection)

* Protects app during runtime
* Blocks attacks automatically

---

# 🎯 For SRE / DevSecOps Role

You should know:

✔ How to integrate SAST in CI
✔ How to automate DAST in staging
✔ How to fail pipeline on critical issues
✔ How to reduce false positives
✔ How to prioritize CVSS score

---

# 🏆 Final Simple Summary

> SAST = Secure the code
> DAST = Secure the running application

You need BOTH for production-grade DevSecOps.

---

If you want next, I can explain:

* 🔥 How to integrate OWASP ZAP in Jenkins
* 🛠 How to reduce false positives in SonarQube
* 📊 How companies design security gates
* 💼 SAST/DAST interview questions

Tell me your goal.
