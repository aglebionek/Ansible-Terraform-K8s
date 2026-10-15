# Manual scheduling
A pod can be scheduled to a specific node by specifying the `nodeName` field in the pod spec. This is a manual scheduling method and should be used with caution, as it bypasses the scheduler's decision-making process.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: manual-scheduled-pod
spec:
  nodeName: <node-name> # Replace with the name of the desired node, like node01
```

# Node labels and selectors

## Node labels
We can add labels to nodes that can be used to select nodes for scheduling pods.

```bash
kubectl label node <node-name> <label-key>=<label-value>
```

## Node selectors
We can use node selectors in the pod spec to specify that a pod should be scheduled on nodes with specific labels.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: node-selector-pod
spec:
  nodeSelector:
    <label-key>: <label-value> # Replace with the label key and value you want
```

## Limitations of node selectors
Node selectors are a simple way to constrain pods to nodes with specific labels, but they have some limitations. They just allow to match a single label, but multiple labels or logical operators are not possible. For that, we use node affinity.

# Node affinity

## Example of node affinity
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: node-affinity-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: "<label-key>" # Replace with the label key you want to match
            operator: "In" # Can be In, NotIn, Exists, DoesNotExist, GreaterThan, or LessThan
            values:
            - "<label-value>" # Replace with the label value you want to match
```

## Node affinity
DuringScheduling - apply when scheduling a pod, before it exists.
DuringExecution - applies to already running pods.
requiredDuringScheduling - hard requirement, pod will not be scheduled if not met.
preferredDuringScheduling - soft requirement, pod wil

Refer to documentation for more details on node affinity: https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity
