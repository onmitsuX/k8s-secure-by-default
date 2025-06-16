🔐 Kubernetes Secure-by-Default Policies
========================================

This repository contains real-world Kubernetes admission control policies using [OPA Gatekeeper](https://open-policy-agent.github.io/gatekeeper/). Each folder includes a secure-by-default policy that aligns with best practices from:

-   CIS Kubernetes Benchmarks

-   NIST 800-190

-   Zero Trust Principles

All policies are tested on Minikube and designed to block insecure deployments before they reach production.

* * * * *

🚀 Use Cases Covered
--------------------

| Policy | Description |
| 🛑 Deny Privileged Containers | Blocks containers with `securityContext.privileged: true` |
| ✅ Enforce TLS on Services | Requires services to use HTTPS ports (e.g., 443) |
| 🔐 Require Non-Root Users | Enforces `runAsNonRoot: true` in container securityContext |
| 📋 Require Resource Limits | Enforces `resources.limits` for CPU and memory |
| 🔄 Disallow Latest Image Tag | Blocks containers using the `:latest` image tag |

* * * * *

🗂 Folder Structure
-------------------

```
.
├── 01-deny-privileged-containers/
├── 02-enforce-tls-service/
├── 03-require-non-root-containers/
├── 04-kube-bench/
├── 05-require-resource-limits/
├── 06-disallow-latest-tag/
├── .github/
│   └── workflows/
│       └── gatekeeper-ci.yml
└── README.md
```

Each folder contains:

-   `ConstraintTemplate` with Rego logic

-   `Constraint` to apply enforcement

-   ✅ Compliant and ❌ violating test manifests

-   `README.md` with explanation and testing steps

* * * * *

🧪 How to Test Locally
----------------------

Apply the policies on any Kubernetes cluster (Minikube, Kind, EKS, AKS, etc):

```
kubectl apply -f constrainttemplate.yaml
kubectl apply -f constraint.yaml
kubectl apply -f test-pod.yaml  # Should fail or pass depending on policy
```

To test with [Conftest](https://www.conftest.dev/):

```
conftest test <manifest>.yaml
```

* * * * *

🔍 Auditing with kube-bench
---------------------------

The `04-kube-bench/` directory includes a Job manifest to run `[kube-bench](https://github.com/aquasecurity/kube-bench)` against the CIS Kubernetes Benchmark.

```
kubectl apply -f 04-kube-bench/kube-bench.yaml
```

View results with:

```
kubectl logs job/kube-bench
```

* * * * *

✅ CI Integration
----------------

GitHub Actions is used to run policy compliance checks on all test manifests via `conftest`.

CI Badge:

![Gatekeeper CI](https://github.com/onmitsuX/k8s-secure-by-default/actions/workflows/gatekeeper-ci.yaml/badge.svg)


* * * * *

📬 Contributions
----------------

This project is actively maintained as a security engineering reference. PRs and suggestions are welcome.