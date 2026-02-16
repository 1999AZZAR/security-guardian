---
name: security-guardian
description: Secure your projects by scanning for hardcoded secrets, API keys, and container vulnerabilities. Use when: (1) Running a security audit on a codebase, (2) Before committing/pushing code to ensure no credentials are leaked, (3) Scanning Docker images for vulnerabilities (CVEs) using Trivy, (4) Implementing security guardrails in CI/CD or deployment workflows.
---

# Security Guardian

System for automated security auditing and credential protection. Provides deterministic scanning for hardcoded secrets and container vulnerabilities.

## Core Workflows

### 1. Secret Scanning
Scan directories for hardcoded keys, passwords, and tokens before repository operations or deployments.
- **Tool**: `scripts/scan_secrets.py`
- **Usage**: `python3 scripts/security-guardian/scripts/scan_secrets.py <path_to_project>`
- **Behavior**: If secrets are detected (exit code 1), identify the file and line, then transition credentials to `mema-vault`.

### 2. Container Vulnerability Scan
Analyze Docker images for security vulnerabilities (CVEs) prior to production deployment.
- **Tool**: `scripts/scan_container.sh`
- **Usage**: `bash scripts/security-guardian/scripts/scan_container.sh <image_name>`
- **Logic**: Identify `HIGH` and `CRITICAL` severities. Recommend base image updates (e.g., switching to `-slim` or `-alpine`) or security patches.

### 3. Security Standards
- **Credential Isolation**: Enforce zero-trust by removing plaintext secrets from source code.
- **Attack Surface Reduction**: Favor minimal base images to reduce potential exploit vectors.
- **Periodic Auditing**: Execute recursive scans across deployment directories to maintain a clean state.

## Reference
- **Secrets to watch**: Gemini API Keys, NextDNS IDs, Resend Keys, Database Passwords, SSH Keys.
- **Exclusion**: Always exclude `.git`, `node_modules`, and `venv` from scans to save time.

---
"Brevity never excuses vulnerability." - Identity Protocol
