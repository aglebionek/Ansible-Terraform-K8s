## Persistent Data

### Volumes
Volumes are managed by Docker. They cannot be accessed directly from the host filesystem, nor modified outside of the docker filesystem.

### Bind Mounts
Bind mounts allow us to mount a host directory directly to the container. Any changes made to the files in the host directory will be reflected in the container, and vice versa. 

## Users and processes

### Processes
Docker containers are not VMs, and they are not entirely isolated from the host.
They share the same kernel, meaning that a process in a container is also a process in the host. Running `ps aux` in the host will show all processes, including those running in containers. 
Running `ps aux` in a container will show only the processes running in that container. However, the process IDs will be different. That's because a container has its own PID namespace.

### Users
Docker runs as root by default. However, that root user has limited privileges compared to the host root.
You can modify the container root user permissions:
```bash
docker run --cap-add=<capability> # adds a capability to the container root user
docker run --cap-drop=<capability> # removes a capability from the container root user
docker run --privileged # gives the container root user all capabilities
```

You can also change the user that runs the container.
```bash
docker run -u <user> # runs the container as the specified user
docker run -u <user>:<group> # runs the container as the specified user and group
docker run -u <uid>:<gid> # runs the container as the specified user and group IDs
```

```Dockerfile
# Dockerfile
FROM alpine:latest
RUN addgroup -S mygroup && adduser -S myuser -G mygroup
USER myuser:mygroup
```