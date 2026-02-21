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


## Code Quality checks:

No problem 👍 Let’s simplify everything.

## 💡 What are Code Quality Checks?

It just means:

> Checking if your code is **clean, correct, and safe** before deploying.

That’s it.

---

# 🧹 Imagine This

You write code.

Before deploying, we check:

1. ❌ Is there any syntax mistake?
2. ❌ Is the code messy?
3. ❌ Are there bugs?
4. ❌ Is it insecure?
5. ❌ Are there vulnerable libraries?

If all good → deploy
If not → fix first

That process = **Code Quality Check**

---

# 🔎 4 Main Types (Very Simple)

## 1️⃣ Linting

Checks style & small mistakes.

Example:

* Unused variable
* Missing semicolon
* Wrong indentation

Tool example:

* ESLint

---

## 2️⃣ Unit Testing

Checks if your logic works.

Example:
You create a function:

```text
add(2,3)
```

Test checks:
Expected result = 5
If not → fail

---

## 3️⃣ Static Code Analysis

Deeper check.

Finds:

* Big functions
* Duplicate code
* Security problems

Tool example:

* SonarQube

---

## 4️⃣ Dependency Check

Checks if libraries have vulnerabilities.

Tool example:

* OWASP Dependency-Check

---

## 4️⃣ Security Checks (SAST)

Finds:

SQL injection

Hardcoded passwords

XSS

Unsafe deserialization

Example:

SonarQube

Semgrep

This connects quality + security.

## 6️⃣ Performance & Efficiency Checks

Advanced quality includes:

Memory leaks

Inefficient loops

Blocking operations

Slow queries

Tools:

Profilers

Load testing tools

# 🚦 In CI/CD Pipeline

When you push code:

```text
1. Lint
2. Test
3. Quality Scan
4. Security Scan
5. Deploy
```

If any step fails → ❌ Stop

That protects production.

---

# 🧠 Why It Is Important?

Without quality checks:

* More bugs
* Production failures
* Security issues
* Hard maintenance

With quality checks:

* Stable app
* Clean code
* Secure deployment

---

# 🎯 One-Line Summary

> Code quality checks = Automatic inspection of your code before deployment to avoid bugs and security issues.

---

Tell me — what part is confusing?

* Lint?
* SonarQube?
* Coverage?
* Technical debt?
* Quality gate?

I’ll explain only that in very simple way.

