# Security Context
In Docker, the default user that runs the container is root. However, in Kubernetes, the default user is a non-root user. This is done for security reasons, as running containers as root can pose a security risk.

You can specify the user that runs the container at the pod level.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  securityContext:
    runAsUser: 1000 # User ID
    runAsGroup: 3000 # Group ID
  containers:
  - name: mycontainer
    image: nginx
```

However, Docker allows you to specify the user and their capabilities at container level. 
You can also do that in Kubernetes. 
Container level user/capabilities overrides the pod level user.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  securityContext:
    runAsUser: 1000 # User ID
    runAsGroup: 3000 # Group ID
  containers:
  - name: mycontainer
    image: nginx
    securityContext: # This is container level, and thus will override the pod level security context
      runAsUser: 2000 # User ID
      runAsGroup: 4000 # Group ID
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"] # Add capabilities to the container
        drop: ["MKNOD"] # Drop capabilities from the container
```