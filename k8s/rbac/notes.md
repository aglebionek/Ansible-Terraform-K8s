### RBAC - Role-Based Access Control
- A method for regulating access to resources based on the roles of individual users within an organization.
- In Kubernetes, RBAC is used to control who can access the Kubernetes API and what actions they can perform.

<img src="rbac.png" alt="RBAC Diagram" style="width:600px;"/>

### Key Concepts
- **Role** and **ClusterRole** are K8s Objects that define a set of permissions.
- **Role** is namespace-scoped, while **ClusterRole** is cluster-scoped.

- **RoleBinding** Objects connect Roles to users.
- **ClusterRoleBinding** Objects connect ClusterRoles to users.

### yaml Examples 
https://kubernetes.io/docs/reference/access-authn-authz/rbac/

- Role Example:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

- RoleBinding Example:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
# This role binding allows "jane" to read pods in the "default" namespace.
# You need to already have a Role named "pod-reader" in that namespace.
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
# You can specify more than one "subject"
- kind: User
  name: jane # "name" is case sensitive
  apiGroup: rbac.authorization.k8s.io
roleRef:
  # "roleRef" specifies the binding to a Role / ClusterRole
  kind: Role #this must be Role or ClusterRole
  name: pod-reader # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
```
