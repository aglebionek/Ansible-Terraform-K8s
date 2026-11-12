# Network Policies

By default, all pods in a cluster can communicate with each other. Network policies let us restrict this communication for security reasons.

Network policies work as **allowlists**:

- A policy selects the pods it applies to and the traffic directions it restricts.
- For those directions, traffic is blocked unless a rule allows it.
- If multiple policies select a pod, their allowed traffic is combined. One policy cannot override another policy’s allowance.

## Ingress and Egress

Network communication has two directions:

- **Ingress**: Incoming traffic to a pod.
- **Egress**: Outgoing traffic from a pod.

This is in regard to where the traffic originates from, not where it is going. For example, a pod that receives traffic from another pod has **ingress** traffic, while the sending pod has **egress** traffic.
Reply traffic for an allowed connection is automatically allowed. An ingress-only policy does not restrict connections initiated by the selected pod.

## Network Policy Examples

### Allow frontend pods to access the database

This policy restricts incoming traffic to pods labeled `app=database` in the `default` namespace. It allows connections from pods labeled `app=frontend` in that same namespace, on TCP port `3306`.

Other incoming traffic is blocked unless another policy allows it.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend-to-database
  namespace: default
spec:
  # Select the pods whose traffic will be restricted.
  podSelector:
    matchLabels:
      app: database
  policyTypes:
  - Ingress
  ingress:
  - from:
    # Without a namespaceSelector, this matches only pods
    # in the same namespace as this NetworkPolicy.
    - podSelector:
        matchLabels:
          app: frontend
    ports:
    - protocol: TCP
      port: 3306
```

To explicitly specify the source namespace, use both selectors in the **same `from` item**. Both must match:

```yaml
    - podSelector:
        matchLabels:
          app: frontend
      namespaceSelector:
        matchLabels:
          kubernetes.io/metadata.name: default
```

### Block all incoming connections to the database

This policy selects database pods for ingress isolation and provides no allowed ingress rules.

Incoming connections are blocked unless another policy allows them. Connections initiated by the database pods remain unrestricted by this policy.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all-ingress-to-database
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: database
  policyTypes:
  - Ingress
  ingress: []
```

**Important:** `ingress: []` allows no incoming connections, while `ingress: [{}]` allows all incoming connections.

These rules require a network plugin that supports NetworkPolicy. Kubernetes also has specific exceptions, including traffic from a pod’s own node. See the [Kubernetes NetworkPolicy documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/).
