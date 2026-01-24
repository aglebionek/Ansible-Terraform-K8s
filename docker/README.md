## Persistent Data

### Volumes
Volumes are managed by Docker. They cannot be accessed directly from the host filesystem, nor modified outside of the docker filesystem.

### Bind Mounts
Bind mounts allow us to mount a host directory directly to the container. Any changes made to the files in the host directory will be reflected in the container, and vice versa. 