---
name: k8s-monitor
description: Monitor and debug Kubernetes deployments on GKE. Use for checking pod status, viewing logs, rollout status, scaling, and troubleshooting deployment issues.
---

# K8s Monitor

Monitor and debug Kubernetes deployments.

## Prerequisites

- `kubectl` configured with cluster access
- `gcloud` authenticated for GKE

## Quick Reference

### Check deployment status
```bash
kubectl get deployments -n <namespace>
kubectl rollout status deployment/<name> -n <namespace>
```

### View pods and their status
```bash
kubectl get pods -n <namespace> -l app=<app-label>
kubectl describe pod <pod-name> -n <namespace>
```

### View logs
```bash
# Current logs
kubectl logs -n <namespace> -l app=<app-label> --tail=100

# Previous container (after crash)
kubectl logs -n <namespace> <pod-name> --previous

# Follow logs
kubectl logs -n <namespace> -l app=<app-label> -f
```

### Troubleshooting

```bash
# Events (useful for crash debugging)
kubectl get events -n <namespace> --sort-by='.lastTimestamp' | tail -20

# Resource usage
kubectl top pods -n <namespace>

# Describe for detailed state
kubectl describe deployment/<name> -n <namespace>
```

### Rollback
```bash
# View history
kubectl rollout history deployment/<name> -n <namespace>

# Rollback to previous
kubectl rollout undo deployment/<name> -n <namespace>

# Rollback to specific revision
kubectl rollout undo deployment/<name> -n <namespace> --to-revision=<N>
```

### Helm operations
```bash
# List releases
helm list -n <namespace>

# Release history
helm history <release-name> -n <namespace>

# Rollback
helm rollback <release-name> <revision> -n <namespace>
```

## NextCMS Specifics

- **Namespace:** `nextcms`
- **Deployment:** `nextcms-backend`
- **Cluster:** `services-sg-prod` (asia-southeast1-a)

```bash
# Quick status check
kubectl get pods -n nextcms -l app=nextcms-backend
kubectl rollout status deployment/nextcms-backend -n nextcms
```
