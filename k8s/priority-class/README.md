# Priority class
In k8s, nodes have limited resources. If having multiple pods, some of the less important pods may take up resources that are needed by more important pods. To avoid this, Kubernetes provides a way to assign priority to pods using priority classes.

```kubectl get priorityclass```
Not namespaced.

## Example

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
description: "This priority class should be used for high priority pods."
value: 100000 # Range between 1 000 000 000 and -2 147 000 000. K8s components can have up to 2 000 000 000. By default all pods have a priority of 0.
globalDefault: false # Setting this to true will make this priority class the default for all pods that do not have a priority class specified. Only one priority class can be the default.
preemptionPolicy: PreemptLowerPriority # This option will kill lower priority pods to make room for higher priority pods. The other option is Never, which will not preempt lower priority pods.
---

apiVersion: v1
kind: Pod
metadata:
  name: high-priority-pod
spec:
  priorityClassName: high-priority
```