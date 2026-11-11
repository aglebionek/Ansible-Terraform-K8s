# Network Policies
By default, all pods in a cluster can communicate with each other.
We might want to restrict this communication for security reasons. 
Network policies allow us to control the traffic flow between pods and namespaces.

## Ingress and Egress
You can seperate the network communication into two types:
- **Ingress**: Incoming traffic to a pod.
- **Egress**: Outgoing traffic from a pod.

### Network Policy Example
```yaml
# Block database from receiving incoming traffic from frontend pods
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: block-frontend-to-database
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: database
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend
```