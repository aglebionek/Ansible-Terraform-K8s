# Node goes down
If a node is down for 50 seconds by default, it's marked as NotReady. It means that the node is not available for scheduling new pods. The default timeout can be configured by changing the `node-monitor-grace-period` parameter in the kube-controller-manager.
If a node is marked as NotReady, the node controller adds taints to the node to prevent new pods from being scheduled on it.

If a node is down for 5 minutes by default, it's marked as Unreachable. It means that the node is not available for scheduling new pods and the pods running on that node are considered lost. The default timeout can be configured by changing the `pod-eviction-timeout` parameter in the kube-controller-manager.

Depending on the way the pods are set up, they can be rescheduled to other nodes or they can be lost. If the pods are part of a Deployment, ReplicaSet, StatefulSet, etc., they will be rescheduled to other nodes. If the pods are standalone pods, they will be lost.

# Simulating node downtime
You can simulate node downtime.

```bash
kubectl cordon <node-name> # mark the node as unschedulable, but keep the pods running
kubectl drain <node-name> # mark the node as unschedulable and evict the pods from the node
kubectl uncordon <node-name> # mark the node as schedulable again
```

If a node to drain has pods not part of replica sets, deployments, or stateful sets, the drain command will fail. You can use the `--force` flag to force the eviction of those pods.