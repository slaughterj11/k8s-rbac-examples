# Incident Responder

Temporary elevated access for debugging production issues. Provides read access across the cluster with targeted write permissions for common incident response actions like restarting pods and scaling deployments.

## What It Grants

- Read access to pods, logs, events, services, configmaps across all namespaces
- Exec into pods for live debugging
- Delete pods (force restart stuck workloads)
- Scale deployments up or down (for capacity response)
- Read access to nodes (for infrastructure visibility)
- Read access to network policies and ingresses

## What It Does Not Grant

- No create or delete on deployments, services, or configmaps
- No secret access
- No RBAC modifications
- No node management (cordon, drain)

## When To Use

- On call engineers responding to production incidents
- Temporary access during P1/P2 escalations
- Break glass scenarios where quick debugging is needed

## Important

This role is labeled `temporary: "true"` as a reminder to revoke it after the incident is resolved. Consider automating the creation and cleanup of this binding through your incident management workflow.

## Usage

Grant access at the start of an incident:

```bash
kubectl apply -f incident-responder/
```

Revoke access after the incident:

```bash
kubectl delete -f incident-responder/binding.yaml
```
