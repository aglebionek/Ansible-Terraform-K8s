# Images in containers

Whenever you create a Kubernetes object like a pod, you specify the image. For example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: nginx # Image here
```

This way of specifing an image hides some important details.
A full image specification follows:
```
<registry_url>/<repository>/<image>:<tag>
```

In the `nginx` example:
1. The registry is `docker.io` (the default docker registry)
2. The repository is `library` (the default repository for official images)
3. The image is `nginx`
4. The tag is `latest` (the default tag if none is specified)

## Private registries and K8S
You can host a private registry to store your images.
However, you have to log in to a registry to be able to access the images.
Kubernetes allows you to do that by creating a secret with your credentials and then referencing that secret in your pod definition.

```bash
kubectl create secret docker-registry <secret_name> \
  --docker-server=<registry_url> \
  --docker-username=<username> \
  --docker-password=<password> \
  --docker-email=<email>
```

Then you can reference the secret in your pod definition:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: mycontainer
    image: <registry_url>/<repository>/<image>:<tag>
  imagePullSecrets:
  - name: <secret_name>
```