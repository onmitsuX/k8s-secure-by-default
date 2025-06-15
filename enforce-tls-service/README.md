# 🛡️ Enforce TLS on LoadBalancer Services

## Overview

This Gatekeeper policy enforces that all Kubernetes `Service` objects of type `LoadBalancer` must include a TLS certificate annotation. This ensures that services exposed to the internet follow encryption best practices by default.

---

## 📂 Files

| File | Description |
|------|-------------|
| `tls-service-template.yaml` | Defines the Rego policy logic for checking TLS annotations |
| `require-tls-service.yaml` | Applies the policy to all `Service` objects |
| `insecure-service.yaml` | Test case without TLS annotation (should be denied) |
| `secure-service.yaml` | Test case with TLS annotation (should be allowed) |

---

## 🚀 Apply Policy

```bash
kubectl apply -f tls-service-template.yaml
kubectl apply -f require-tls-service.yaml
