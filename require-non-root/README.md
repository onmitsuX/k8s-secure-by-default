# 🛡️ Enforce Non-Root Containers with Gatekeeper

## Overview

This policy enforces that all containers in Kubernetes pods must run as **non-root users** by checking:

- `securityContext.runAsNonRoot: true` is explicitly set
- `securityContext.runAsUser` is **not** UID `0` (root)

This ensures that even if a container tries to bypass `runAsNonRoot`, it cannot run as UID 0. This aligns with hardening guidelines from [CIS Benchmarks](https://www.cisecurity.org/), [NIST 800-190](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-190.pdf), and many enterprise compliance frameworks.

---

## 📁 Files

| File | Description |
|------|-------------|
| `non-root-template.yaml` | Gatekeeper `ConstraintTemplate` using Rego to block root containers |
| `require-non-root.yaml` | Gatekeeper `Constraint` that applies the policy to all Pods |
| `root-pod.yaml` | Test pod with `runAsNonRoot: false` — should be **denied** |
| `non-root-pod.yaml` | Compliant pod with `runAsNonRoot: true` — should be **allowed** |

---

## 🚀 Usage

### 1. Apply the Template and Constraint

```bash
kubectl apply -f non-root-template.yaml
kubectl apply -f require-non-root.yaml
