Here are clean **GitHub notes without special symbols** so you can directly paste into a README file.

---

# Pre Commit Security Checks DevSecOps Notes

## Overview

Pre commit is a Git hook framework that runs security and code quality checks before code is committed.

It helps implement shift left security by catching issues early on the developer machine.

---

## How it works

```text id="flow1"
Developer writes code
git add
git commit
Pre commit hooks run
If pass commit is allowed
If fail commit is blocked
```

---

## Prerequisites

* Git installed
* Python installed
* Git repository initialized

---

## Step by Step Setup

### 1 Initialize Git repository

```bash id="s1"
git init
```

---

### 2 Install pre commit

```bash id="s2"
pip install pre-commit
```

Check version

```bash id="s3"
pre-commit --version
```

---

### 3 Create configuration file

Create file in repo root

.pre-commit-config.yaml

---

### 4 Add security hooks

```yaml id="s4"
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.6.0
    hooks:
      - id: detect-aws-credentials
      - id: detect-private-key
      - id: check-yaml
      - id: check-json
      - id: trailing-whitespace
      - id: end-of-file-fixer
```

---

## What these checks do

detect aws credentials prevents AWS keys from being committed
detect private key blocks SSH private keys
check yaml validates YAML syntax
check json validates JSON syntax
trailing whitespace removes extra spaces at end of lines
end of file fixer ensures newline at end of file

---

### 5 Install Git hook

```bash id="s5"
pre-commit install
```

This connects pre commit with Git hooks system

---

### 6 Test manually

```bash id="s6"
pre-commit run --all-files
```

---

### 7 Commit code

```bash id="s7"
git add .
git commit -m "test pre commit"
```

---

## Expected Output

### Success

detect aws credentials PASS
detect private key PASS
check yaml PASS

### Failure

FAILED detect private key

Commit will be blocked until issue is fixed

---

## Important Notes

* Hooks run only if pre commit install is executed
* You can bypass checks using git commit no verify
* YAML indentation must be correct
* Works only inside Git repository

---

## DevSecOps Flow

```text id="flow2"
Pre commit
CI pipeline
SAST scanning
DAST scanning
Deployment
```

---

## Optional Enterprise Tools

* Gitleaks for secret scanning
* Bandit for Python security
* Semgrep for multi language scanning
* Black or Prettier for formatting

---

## Summary

Pre commit runs checks before commit
Prevents secrets from entering repository
Enforces code quality rules
First security layer in DevSecOps pipeline

---

If you want, I can also convert this into a polished GitHub README with badges and real project structure.
