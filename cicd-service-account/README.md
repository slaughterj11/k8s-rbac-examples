# CI/CD Service Account

Scoped permissions for deployment pipelines. This service account can create and update deployments, services, configmaps, and ingresses but cannot delete critical resources or modify RBAC.

## What It Grants

- Create, update, and patch deployments (including scale)
- Create, update, and patch services, configmaps, and ingresses
- Read only access to secrets (for pulling image credentials)
- Read access to pods and pod logs (for deployment verification)
- Create and delete jobs (for migration tasks)

## What It Does Not Grant

- No delete on deployments, services, or configmaps (prevent accidental teardown)
- No create or update on secrets (managed separately)
- No exec into pods
- No RBAC modifications
- No access to other namespaces

## When To Use

- GitHub Actions, GitLab CI, Jenkins, or ArgoCD service accounts
- Any automated pipeline that deploys to a specific namespace
- Environments where you want pipelines to deploy but not destroy

## Usage

```bash
kubectl apply -f cicd-service-account/
```

Generate a kubeconfig for the service account:

```bash
kubectl create token cicd-deployer -n team-alpha --duration=1h
```
