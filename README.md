# 🔐 Kubernetes Security Policies with OPA Gatekeeper

This repository contains real-world Kubernetes admission control policies using [OPA Gatekeeper](https://open-policy-agent.github.io/gatekeeper/). Each folder is a secure-by-default policy that aligns with best practices like:

- CIS Kubernetes Benchmarks
- NIST 800-190
- Zero Trust Principles

All policies are tested on Minikube and designed to block insecure deployments before they reach production.

---

## 🚀 Use Cases Covered

| Policy | What it Does |
|--------|---------------|
| 🛑 Deny Privileged Containers | Blocks pods with `securityContext.privileged: true` |
| ✅ Enforce TLS on Services | Requires TLS annotation for `LoadBalancer` services |
| 🔐 Require Non-Root Users | Ensures `runAsNonRoot: true` and UID ≠ 0 |
| 📋 (Coming Soon) Require Resource Limits | Enforce CPU/memory limits per container |
| 🔄 (Coming Soon) Disallow `latest` image tag | Forces immutable image versions |

---

## 🗂 Folder Layout

Each folder contains:
- `ConstraintTemplate` with Rego logic
- `Constraint` to apply enforcement
- ✅ Compliant and ❌ violating test pods
- `README.md` with explanation and testing steps

---

## 🧪 How to Test Locally

You can apply these on any Kubernetes cluster (Minikube, Kind, EKS, AKS, etc):

```bash
kubectl apply -f constrainttemplate.yaml
kubectl apply -f constraint.yaml
kubectl apply -f test-pod.yaml  # Should fail or pass depending on policy
