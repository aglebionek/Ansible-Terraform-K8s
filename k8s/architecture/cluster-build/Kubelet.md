# Kubelet

<img src="./full-diagram.png" alt="full-diagram" width="600"/>

Kubelet is an agent running on each worker node in the cluster.

## Kubelet's Responsibilities
1. Kubelet registers the node with the kube-apiserver.
2. Kubelet watches for pod specifications via the kube-apiserver. It can request the container runtime to pull/create/start containers based on the pod specifications.
3. It monitors the state of the containers and reports back to the kube-apiserver.