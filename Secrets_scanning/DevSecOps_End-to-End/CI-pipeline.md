```
Developer Commit
        ↓
Pre-commit checks (local)
        ↓
Push to Git repository
        ↓
CI Pipeline Trigger (Jenkins / GitHub Actions)
        ↓
1. Source Checkout
        ↓
2. Code Quality Check
        ↓
3. Build Stage
        ↓
4. Unit Testing
        ↓
5. SAST Security Scan
        ↓
6. Dependency Scan (SCA)
        ↓
7. Artifact Creation
        ↓
8. Artifact Storage
        ↓
9. Approval / Quality Gate
        ↓
Ready for CD (Deployment pipeline)
```
