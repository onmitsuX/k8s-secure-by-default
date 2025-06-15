# 🔄 Disallow `:latest` Image Tag

## Overview

This policy enforces image immutability by blocking containers using the `:latest` image tag. Deploying unversioned images leads to inconsistent builds, lack of traceability, and production instability.

## 📁 Files

- `constrainttemplate.yaml`: Rego logic to detect `:latest` tags
- `constraint.yaml`: Applies enforcement to all pods
- `latest-image-pod.yaml`: Should be blocked
- `versioned-image-pod.yaml`: Should be allowed

## 🚀 Usage

```bash
kubectl apply -f constrainttemplate.yaml
kubectl apply -f constraint.yaml
