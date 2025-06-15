# 🔐 Deny Privileged Containers (OPA Gatekeeper)

## Overview

This Gatekeeper policy enforces that no container in a Kubernetes Pod may run with `securityContext.privileged: true`. Privileged containers have elevated access to the host system, posing a serious security risk and violating best practices under CIS Benchmarks and NIST 800-190.

---

## 🎯 Purpose

Prevent escalation of privileges by ensuring workloads do not run with `privileged` mode enabled. This helps reduce the blast radius in the event of a compromise and enforces container isolation as part of your platform security baseline.

---

## 📁 Files

| File | Description |
|------|-------------|
| `constrainttemplate.yaml` | Rego policy logic to detect privileged containers |
| `constraint.yaml` | Applies the policy to all Pods in the cluster |
| `privileged-pod.yaml` | Example Pod that should be denied |
| `README.md` | This documentation file |

---

## 🚀 Usage

### 1. Apply the Gatekeeper Template and Constraint

```bash
kubectl apply -f constrainttemplate.yaml
kubectl apply -f constraint.yaml
