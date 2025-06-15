# kube-bench: CIS Benchmark Check for Kubernetes

## Purpose
Run kube-bench to check the current Kubernetes environment against the CIS Kubernetes Benchmark. This helps identify misconfigurations that may lead to privilege escalation, insecure components, or lack of proper auditing.

## Files
- `kube-bench.yml`: Job definition to run kube-bench as a Kubernetes Job
- `kube-bench-report.json`: Output report from the job (use `kubectl logs` or redirect)

## How to Run

```bash
kubectl apply -f kube-bench.yaml
kubectl logs job/kube-bench -n kube-system > kube-bench-report.json
