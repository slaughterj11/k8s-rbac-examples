# Namespace Admin

Full control within a single namespace. Intended for team leads and service owners who need to manage all resources in their team's namespace without cluster level access.

## What It Grants

- Full CRUD on core resources: pods, services, configmaps, secrets, PVCs
- Full CRUD on workloads: deployments, replicasets, statefulsets, daemonsets
- Full CRUD on batch: jobs, cronjobs
- Full CRUD on networking: ingresses, network policies
- Full CRUD on autoscaling and disruption budgets

## What It Does Not Grant

- No access to other namespaces
- No cluster scoped resources (nodes, persistent volumes, cluster roles)
- No ability to create or modify RBAC policies
- No access to the kube-system namespace

## When To Use

- Team leads who own a service and need full operational control
- Service owners who deploy, scale, and manage their own workloads
- Environments where teams are isolated by namespace

## Usage

Update the namespace in both files to match your target namespace, then apply:

```bash
kubectl apply -f namespace-admin/
```

Verify:

```bash
kubectl auth can-i --list --as=system:serviceaccount:team-alpha:default -n team-alpha
```
