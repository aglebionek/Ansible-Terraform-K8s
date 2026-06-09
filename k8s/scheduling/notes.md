The `nginx-nodeselector` and `frontend-app` pods in the [example](./example.yml) require a node with label `disktype: ssd` to run. The scheduler will look for a node with that label and schedule the pod on it. If no such node is found, the pod will remain in a pending state until a suitable node becomes available.

```yml
...
spec:
  nodeSelector:
    disktype: ssd
...
```

To add a label to a node, you can use the following command:

```bash
kubectl label nodes <node-name> disktype=ssd
```


Similarly, the `nginx-nodename` pod requires a node with the name `k8s-worder-01` to run.

```yml
...
spec:
  nodeName: k8s-worker-01
...
```

To specify a node by name, you can use the following command: