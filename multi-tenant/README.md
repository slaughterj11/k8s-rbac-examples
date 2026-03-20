# Multi Tenant Isolation

Strict namespace boundaries with no cross namespace visibility. Each tenant gets full control within their own namespace but cannot see or interact with resources in other namespaces.

## What It Grants

- Full CRUD on core resources within the tenant namespace
- Full CRUD on workloads (deployments, replicasets, statefulsets)
- Full CRUD on batch resources (jobs, cronjobs)
- Create and manage ingresses within the namespace

## What It Does Not Grant

- No access to any other namespace
- No cluster scoped resource access
- No secret management (add separately if needed)
- No RBAC modifications

## Network Isolation

This policy includes a NetworkPolicy that blocks all cross namespace traffic by default. Only intra namespace pod communication and DNS resolution (kube-system) are allowed.

## When To Use

- Shared clusters where multiple teams or customers coexist
- Environments that require strict blast radius containment
- Compliance scenarios requiring workload isolation

## Usage

Create the tenant namespace first, then apply:

```bash
kubectl create namespace tenant-a
kubectl apply -f multi-tenant/
```

Repeat for each tenant, updating the namespace in all files.
