## Resource Request 
- A request for the resources (CPU, memory, etc.) that a container needs to run.
- Kube scheduler uses this information to see if there are enough resources available on a node to schedule the pod. If there is not, a resource will not be run.
- Measured in Bytes for memory and in CPU units for CPU (1vCPU is 1000 CPU units).

## Resource Limit
- A limit of the resources that a container can use.
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
      # No limit by default
      # If we set only the limit, the request will be set to the same value as the limit.
      limits:
        memory: "128Mi" # 128 Mebibytes of memory
        cpu: "500m" # 500 milliCPU (0.5 CPU)
```
There are the same as reservations and limits in docker-compose.

## Limit Range
We can create a reusable configuration for resource requests and limits using LimitRange.

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: limit-range-demo
spec:
  limits:
  - type: Container
    default:
      memory: "128Mi"
      cpu: "500m"
    defaultRequest:
      memory: "64Mi"
      cpu: "250m"
    max:
      memory: "256Mi"
      cpu: "1000m"
    min:
      memory: "32Mi"
      cpu: "100m"
```

## Resource Quota
We can limit the total amount of resources that can be used in a namespace using ResourceQuota.

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: resource-quota-demo
spec:
  hard:
    requests.cpu: "2" # 2 CPU
    requests.memory: "4Gi" # 4 Gibibytes of memory
    limits.cpu: "4" # 4 CPU
    limits.memory: "8Gi" # 8 Gibibytes of memory
```
