## Sources for the variable names
- <resource_type> - kind in the resource file, e.g. deployment
- <resource_name> - metadata.name in the resource file, e.g. client-deployment
- <container_name> - containers.name in the resource file, e.g. client
- <new_image> - the full name of the image, including the tag, e.g. stephengrider/multi-client:v5

## Managing resources
- ```kubectl apply -f .``` - applies all configurations in the current directory
- ```kubectl create -f .``` - creates all the configurations in the current directory
- ```kubectl delete -f .``` - deletes all the configurations in the current directory
- ```kubectl delete <resource_type> <resource_name>``` - deletes a specific resource

## Generating resource yaml files
- ```kubectl run <resource name> --image=<image name> --dry-run=client -o yaml``` - get a starting yaml definition for the resource
- ```kubectl create <resource_type> <resource_name> --image=<image name> --dry-run=client -o yaml``` - get a starting yaml definition for the deployment

## Information on resource definitions
- ```kubectl api-resources``` - lists all the resource types available in the cluster
- ```kubectl explain <resource_type>[.field] [--recursive]``` - shows the fields and their descriptions for the specified resource type, use --recursive to see all nested fields. Use .field to see the description of a specific field. For example, ```kubectl explain deployment.spec``` shows the fields in the spec of a deployment, and ```kubectl explain deployment.spec.replicas``` shows the description of the replicas field in the spec of a deployment.

## Exposing resources to the outside world
- ```kubectl expose <resource_type> <resource_name> --type=NodePort|LoadBalancer --port=<service port> --name=<service name>``` - exposes the deployment with a NodePort or LoadBalancer service type. This creates a service that can be accessed from outside the cluster through the minikube IP and nodePort.
- ```kubectl port-forward pod/<pod name> <local port>:<container port>``` - forwards a local port to a pod port, useful for quick testing without creating a Service
- ```kubectl port-forward service/<service name> <local port>:<service port>``` - forwards a local port to a Service
- Example: ```kubectl port-forward pod/two-containers 8080:80``` and then open ```http://localhost:8080```

## Status commands
1. ```kubectl get <resource> <resource name> -o <output> --selector <label selector> --sort-by <JSONpath>``` - lists all the resources, e.g. deployments, pods, services
    - ```-o``` - output format, e.g. yaml, json, wide
    - ```--selector``` - filter by label selector, e.g. app=client
    - ```--sort-by``` - sort by a specific field, e.g. .status.containerStatuses[0].restartCount
    - ```--no-headers``` - don't print headers, useful for scripting or troubleshooting, example ```kubectl get pods --no-headers --selector env=dev | wc -l```
    - ```--custom-columns``` - specify custom columns to display. We can access the fields in the resource definition using JSONPath. For example, ```kubectl get pods --custom-columns=NAME:.metadata.name,PRIORITY_CLASS:.spec.priorityClassName```. So the convention follows ```<COLUMN_NAME>:<JSONPath>```.
2. ```kubectl get all``` - lists all resources in the current namespace
3. ```kubectl describe <resource> <resource name>``` - shows more information about the resource
4. ```kubectl logs <pod name>``` - shows the logs of the pod
5. ```crictl pods``` - lists all the pods in the node, useful for troubleshooting when kubectl is not working

## Updating running resources
edit the pod.yaml file to make changes
```bash
kubectl get pod <pod_name> -o yaml > pod.yaml
kubectl delete pod <pod_name>
kubectl apply -f pod.yaml
```

- ```kubectl set image <resource_type>/<resource_name> <container_name>=<new_image>```
- ```kubectl edit <resource_type>/<resource_name>``` - opens the resource definition in an editor, allowing you to modify it directly
- ```kubectl scale <resource_type>/<resource_name> --replicas=<number_of_replicas>``` - scales the resource to the specified number of replicas
- ```kubectl replace [--force] -f <file>``` - replaces the resource with the definition in the specified file

## Accessing containers inside a node
- ```kubectl exec -it <container_name> -- sh``` - opens a shell inside the container, same as docker exec.

## Configs and contexts
- ```kubectl config get-contexts``` - lists all contexts
- ```kubectl config use-context <context_name>``` - switches to the specified context

## Namespaces
By default the namespace is named 'default'
- ```kubectl get namespaces``` - lists all namespaces
- ```kubectl create namespace <namespace_name>``` - creates a new namespace
- ```kubectl get <resource>``` - lists resources in the default namespace
- ```kubectl get <resource> --namespace <namespace_name>``` - lists resources in the specified namespace
- ```kubectl get <resource> --all-namespaces|-A``` - lists resources in all namespaces
- ```kubectl delete namespace <namespace_name>``` - deletes the specified namespace and all resources in it
- ```kubectl config set-context --current --namespace=<namespace_name>``` - switch the currently active namespace to the specified namespace

## Dockerfile to k8s (CMD, entrypoint)
|Dockerfile|Kubernetes|Example|
|---|---|---|
|ENTRYPOINT|command|["sleep"]|
|CMD|args|["5"]|
