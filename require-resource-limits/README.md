# 📦 Require Resource Limits on Containers

## Overview

This Gatekeeper policy enforces that all containers specify CPU and memory limits. Resource limits help prevent noisy neighbor problems and accidental cluster resource exhaustion.

## 📁 Files

- `constrainttemplate.yaml`: Rego policy to check for resource limits
- `constraint.yaml`: Enforcement object
- `no-limits-pod.yaml`: Violating pod (denied)
- `with-limits-pod.yaml`: Compliant pod (allowed)

## 🚀 Apply Policy

```bash
kubectl apply -f constrainttemplate.yaml
kubectl apply -f constraint.yaml
