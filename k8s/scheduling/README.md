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