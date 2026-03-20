# Platform Ops

Cluster wide read access with limited write permissions for operational tasks. Designed for platform engineering and SRE teams who need visibility across all namespaces and the ability to perform targeted operational actions.

## What It Grants

- Read access to all resources across all namespaces (pods, deployments, services, events, etc.)
- Read access to cluster scoped resources (nodes, namespaces, persistent volumes)
- Write access to configmaps (for operational config changes)
- Delete pods (for restarting stuck workloads)
- Exec into pods (for debugging)
- Read only access to RBAC resources (for auditing)

## What It Does Not Grant

- No create or delete on deployments (teams own their own workloads)
- No secret modification
- No RBAC modification
- No node management (cordon, drain, taint)

## When To Use

- Platform engineering teams responsible for cluster health
- SRE teams who need cross namespace visibility
- Operations teams who triage issues but do not own application deployments

## Usage

```bash
kubectl apply -f platform-ops/
```

This is a ClusterRole and ClusterRoleBinding, so no namespace is needed.
