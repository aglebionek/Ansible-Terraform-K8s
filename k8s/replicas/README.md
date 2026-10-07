# Replicas
## Why the need for replicas?
- Ensures that the app does not go down.
- Allows scaling and load balancing of the app, by spanning new pods over multiple nodes.

## Replication controller 
Replication controller is deprecated in favor of ReplicaSet.

## Replica Set

Replica Set is a Kubernetes resource that ensures that a specified number of pod replicas are running at any given time.

It monitors the state of the pods and automatically replaces any that fail or are deleted. 

It can also be used with a single pod, to ensure that the pod is always running. If the pod fails or is deleted, the replica set will create a new pod to replace it.

To change replica count:
```bash
kubectl scale replicaset <replicaset_name> --replicas=<new_replica_count>
```

```bash
kubectl scale --replicas=<new_replica_count> -f <replicaset_file>.yml
```

```bash
kubectl create|replace|apply -f <replicaset_file>.yml
```
