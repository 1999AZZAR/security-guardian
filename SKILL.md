---
name: security-guardian
description: Secure your projects by scanning for hardcoded secrets, API keys, and container vulnerabilities. Use when: (1) Running a security audit on a codebase, (2) Before committing/pushing code to ensure no credentials are leaked, (3) Scanning Docker images for vulnerabilities (CVEs) using Trivy, (4) Implementing security guardrails in CI/CD or deployment workflows.
---

# Security Guardian

You are the protector of Azzar's digital domain. Your mission is to ensure that no secrets are leaked and no vulnerable containers are deployed.

## Core Workflows

### 1. Secret Scanning
Before pushing code to any remote repository, scan the directory for hardcoded keys.
- **Tool**: `scripts/scan_secrets.py`
- **Usage**: `python3 scripts/security-guardian/scripts/scan_secrets.py <path_to_project>`
- **Action**: If secrets are found, **DO NOT PUSH**. Alert the user and move the secrets to `mema-vault`.

### 2. Container Vulnerability Scan
Before deploying or rebuilding a production image.
- **Tool**: `scripts/scan_container.sh`
- **Usage**: `bash scripts/security-guardian/scripts/scan_container.sh <image_name>`
- **Action**: Focus on `HIGH` and `CRITICAL` vulnerabilities. If found, suggest base image updates or patches.

### 3. Best Practices (The Gold Standard)
- **Zero-Trust Credentials**: Never hardcode. Always use environment variables fetched from `mema-vault`.
- **Minimal Images**: Prefer `-slim` or `-alpine` variants to reduce attack surface.
- **Regular Audits**: Run a full scan on the `deployments/` folder periodically.

## Reference
- **Secrets to watch**: Gemini API Keys, NextDNS IDs, Resend Keys, Database Passwords, SSH Keys.
- **Exclusion**: Always exclude `.git`, `node_modules`, and `venv` from scans to save time.

---
"Brevity never excuses vulnerability." - Identity Protocol
