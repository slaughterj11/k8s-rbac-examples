# Read Only Dev

View only access to pods, logs, and events within a namespace. Designed for developers who need to troubleshoot their applications without the ability to modify anything.

## What It Grants

- Read access to pods and pod logs
- Read access to services, configmaps, events, endpoints, PVCs
- Read access to deployments, replicasets, statefulsets, daemonsets
- Read access to jobs, cronjobs, ingresses, and HPAs

## What It Does Not Grant

- No create, update, or delete on any resource
- No exec into pods
- No access to secrets (intentional for security)
- No port forwarding

## When To Use

- Developers who need to view logs and events for debugging
- On call engineers who need read access across multiple namespaces
- New team members who should observe before getting write access

## Usage

```bash
kubectl apply -f read-only-dev/
```

Verify:

```bash
kubectl auth can-i get pods --as=developer@example.com -n team-alpha
# yes
kubectl auth can-i delete pods --as=developer@example.com -n team-alpha
# no
```
