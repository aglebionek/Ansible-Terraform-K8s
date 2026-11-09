# Service accounts
User accounts are created to allow access and authorization to the K8S API for humans.
Service accounts are used to allow access and authorization to the K8S API for automated processes (bots), and to allows us to identify the process that is making the request to the API server.

## Default service account
When a pod is created, it is automatically assigned a default service account in the same namespace.
This service account is used to provide an identity for the pod when it interacts with the Kubernetes API server. The default service account has limited permissions and is typically used for basic operations.

## Creating a service account
```bash
kubectl create serviceaccount <service-account-name> -n <namespace>
```

OR

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: <service-account-name>
  namespace: <namespace>
automountServiceAccountToken: false # Look at next section `Service account tokens` for more information about this option
---

apiVersion: v1
kind: Pod
metadata:
  name: <pod-name>
  namespace: <namespace>
spec:
  serviceAccountName: <service-account-name>
  automountServiceAccountToken: false # Look at next section `Service account tokens` for more information about this option
```

## Service account tokens
Service accounts are associated with a secret token. 
This token is used to authenticate the service account when it makes requests to the Kubernetes API server. 
The token is automatically mounted into the pod at `/var/run/secrets/kubernetes.io/serviceaccount/token`.

You can disable the auto mounting by setting the `automountServiceAccountToken` field to `false` in the pod spec or the service account.

You can create your own token by running:
```bash
kubectl create token <service-account-name> -n <namespace> --duration=24h
```
You can then use this token to authenticate to the Kubernetes API server by including it in the `Authorization: Bearer` header of your requests.
