## 1. Installation of TruffleHog
```
curl -sSfL https://raw.githubusercontent.com/trufflesecurity/trufflehog/main/scripts/install.sh | sh
trufflehog --version
```

## 2. Basic Commands
### 1. Scan Git repository
```
trufflehog git https://github.com/org/repo
```
### 2. Scan local Git repo
```
trufflehog git .
```
### 3.Scan filesystem (project folder)
```
trufflehog filesystem .
```
### 4. Scan specific branch
```
trufflehog git --branch main https://github.com/org/repo
```
### 5. Only verified secrets (VERY IMPORTANT 🔥)
```
trufflehog git . --results=verified
```
### 6. JSON output
```
trufflehog git . --json
```

### 7. Limit results
```
trufflehog git . --max_depth 50
```
