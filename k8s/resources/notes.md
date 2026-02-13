## Resource Request 
- A request for the resources (CPU, memory, etc.) that a container needs to run.
- Kube scheduler uses this information to see if there are enough resources available on a node to schedule the pod. If there is not, a resource will not be run.
- measured in Bytes for memory and in CPU units for CPU (1vCPU is 1000 CPU units).

## Resource Limit
- A limit on the resources that a container can use.
- If a container tries to use more resources than its limit, it may be throttled (for CPU) or killed (for memory).
- If CPU limit is reached, the container will be throttled, meaning it will be allowed to run but at a reduced speed. 
- If memory limit is reached, the container will be killed and restarted.

## kubernetes config example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resource-demo
spec:
  containers:
  - name: resource-demo-ctr
    image: nginx
    resources:
      requests:
        memory: "64Mi" # 64 Mebibytes of memory
        cpu: "250m" # 250 milliCPU (0.25 CPU)
      limits:
        memory: "128Mi" # 128 Mebibytes of memory
        cpu: "500m" # 500 milliCPU (0.5 CPU)
```
There are the same as reservations and limits in docker-compose.

