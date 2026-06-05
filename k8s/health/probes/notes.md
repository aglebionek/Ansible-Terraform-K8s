# Monitoring Kubernetes Health

## Liveness Probe
- A liveness probe checks if an application is running. If the liveness probe fails, Kubernetes will restart the container.

### Example of an HTTP liveness probe
```
livenessProbe:
    httpGet:
        path: /health
        port: 8080
    initialDelaySeconds: 3
    periodSeconds: 3
    timeoutSeconds: 1
```

### Example of an exec liveness probe
```
livenessProbe:
    exec:
    command:
        - cat
        - /tmp/healthy
    initialDelaySeconds: 5
    periodSeconds: 5
```

## Startup Probe
- A startup probe checks if an application has started. If the startup probe fails, Kubernetes will restart the container. This is useful for applications that take a long time to start.
- Once the startup probe succeeds, the liveness probe will take over and be used to check if the application is still running.

### Example of an HTTP startup probe
```
startupProbe:
    httpGet:
        path: /up
        port: 8080
    failureThreshold: 30 # number of times to retry before giving up
    periodSeconds: 3 # how often to perform the probe
```

## Readiness Probe
- A readiness probe checks if an application is ready to serve traffic. If the readiness probe fails, Kubernetes will stop sending traffic to the container until it passes again.

### Example of an HTTP readiness probe
```
readinessProbe:
    httpGet:
        path: /ready
        port: 8080
    initialDelaySeconds: 5
    periodSeconds: 5
```