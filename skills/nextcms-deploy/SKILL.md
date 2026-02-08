---
name: nextcms-deploy
description: Deploy NextCMS backend to GKE. Use for triggering deployments, checking deploy status, and managing releases.
---

# NextCMS Deploy

Quick deploy commands for NextCMS backend.

## Repository
- **Path:** `~/code/nextcms`
- **GitHub:** `ngtrvu/nextcms`

## Deployment Info
- **Cluster:** `services-sg-prod` (asia-southeast1-a)
- **Namespace:** `nextcms`
- **Image:** `asia-southeast1-docker.pkg.dev/stagvn/tinilab/nextcms-backend`

## Deploy Commands

### Via GitHub Actions (preferred)
Push to `main` branch triggers auto-deploy:
```bash
cd ~/code/nextcms
git push origin main
```

Check workflow status:
```bash
gh run list --branch main --limit 5
gh run view <run-id>
```

### Manual Deploy with Skaffold
```bash
cd ~/code/nextcms
export IMAGE=asia-southeast1-docker.pkg.dev/stagvn/tinilab/nextcms-backend:$(git rev-parse --short HEAD)
skaffold run -p prod --tag=$(git rev-parse --short HEAD)
```

### Verify Deployment
```bash
kubectl rollout status deployment/nextcms-backend -n nextcms --timeout=120s
kubectl get pods -n nextcms -l app=nextcms-backend
```

### Rollback
```bash
# Via Helm
helm rollback nextcms-backend -n nextcms

# Via kubectl
kubectl rollout undo deployment/nextcms-backend -n nextcms
```

## Key Files
- Dockerfile: `apps/backend/Dockerfile`
- Helm chart: `deploy/backend/`
- Skaffold: `deploy/skaffold.yaml`
- Values: `deploy/backend/values-prod.yaml`
- GHA workflow: `.github/workflows/deploy-backend.yml`

## Secrets Required
- `GCP_SA_KEY` — GCP service account JSON (in GitHub secrets)
