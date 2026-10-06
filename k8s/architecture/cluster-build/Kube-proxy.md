# Kube-proxy

Every pod can reach every other pod. This is achieved via the pod network, which spans all nodes in the cluster. It allows pods to communicate with each other across nodes.

The pods can reach each other directly using their IP addresses. However, pods are ephemeral and can be created and destroyed dynamically. This means that the IP address of a pod can change over time, making it difficult for other pods to reliably communicate with it.

Services provide a stable IP address for a pod. Other pods can call the stable IP address of the service, and the request will be routed to the appropriate pod. This allows pods to communicate with each other without needing to know the IP addresses of individual pods.

The service however does not join the pod network, because it's not a pod. It is a virtual IP address that is managed by the kube-proxy, existing only in the cluster's memory.

Kube-proxy is a process on each node that looks for created services and sets up the necessary rules to route traffic.