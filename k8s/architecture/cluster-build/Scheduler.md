# Kube-scheduler

<img src="./full-diagram.png" alt="architecture_diagram" width="600"/>

Kube-scheduler selects which pod goes on which worker node based on resource availability and other constraints. 
It does NOT create the pod - that's the job of the kubelet on the worker node. The scheduler only assigns a pod to a worker node.

The scheduler looks at the pod's resource requirements, the current state of the cluster, and any constraints or policies that have been defined. It then selects the best worker node for the pod and updates the kube-apiserver with that information.
