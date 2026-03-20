# k8s-rbac-examples

Production ready Kubernetes RBAC policy examples for common enterprise patterns. Each example is self contained and ready to apply to any cluster.

## Policies

| Policy | Directory | Use Case |
|--------|-----------|----------|
| Namespace Admin | `namespace-admin/` | Full control within a single namespace. Common for team leads and service owners. |
| Read Only Dev | `read-only-dev/` | View only access to pods, logs, and events. Safe access for developers during troubleshooting. |
| CI/CD Service Account | `cicd-service-account/` | Scoped permissions for deployment pipelines. Create, update, and rollback deployments and services. |
| Multi Tenant Isolation | `multi-tenant/` | Strict namespace boundaries with no cross namespace visibility. Ideal for shared clusters. |
| Platform Ops | `platform-ops/` | Cluster wide read access with write permissions limited to operational resources like configmaps and secrets. |
| Incident Responder | `incident-responder/` | Temporary elevated access for debugging production issues. Read pods, exec into containers, view logs. |

## Usage

### Apply a policy

\`\`\`bash
kubectl apply -f <policy-directory>/
\`\`\`

### Verify permissions

\`\`\`bash
kubectl auth can-i --list --as=system:serviceaccount:<namespace>:<service-account>
\`\`\`

### Test with impersonation

\`\`\`bash
kubectl get pods --as=<username> -n <namespace>
\`\`\`

## Structure

Each policy directory contains:

- \`role.yaml\` or \`clusterrole.yaml\`: The permission definitions
- \`binding.yaml\`: The RoleBinding or ClusterRoleBinding
- \`README.md\`: What the policy does, when to use it, and what it grants

## Prerequisites

1. \`kubectl\` configured to point at your target cluster
2. Cluster admin permissions to create Roles, ClusterRoles, and Bindings
3. Target namespaces must exist before applying namespace scoped policies

## Notes

These are starting points, not production policies. Review and adjust resource lists, verbs, and scope to match your environment before applying. Always test with \`kubectl auth can-i\` before granting to real users.
