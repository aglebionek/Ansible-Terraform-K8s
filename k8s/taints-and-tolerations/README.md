# Taints and tolerations
Simply put, this applies to putting pods on nodes.

If we want to prevent some pods from being scheduled on certain nodes, we can use taints.

Taints apply to nodes. We can "taint" a node, making it "unfriendly" to all pods.
Tolerations apply to pods. We can make a pod tolerant to a taint, making a node accept the tolerant pod to be scheduled on it.

An example would be the master node in a Kubernetes cluster. We don't want the scheduler to put any pods on this. The master node is pre-tainted to achieve this. If we want to put a pod on the master node, we need to add a toleration to the pod.

## Apply a taint to a node
```bash
kubectl taint nodes <node name> <key>=<value>:<taint effect>[-] 
```

Taint effect can be one of the following:
- NoSchedule - as on the example above, hard requirement
- PreferNoSchedule - as on the example above, soft requirement, no guarantee
- NoExecute - as on the example above, hard requirement, but also evicts any existing pods that do not tolerate the taint

The trailing `-` is optional, and it means to remove the taint rather than apply it.