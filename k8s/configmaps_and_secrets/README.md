# ConfigMap

## Imperative

```bash
kubectl create configmap <configmap_name> --from-literal=<key>=<value>
kubectl create configmap <configmap_name> --from-file=<file_path>
```

## Declarative
[Example configmap.yaml](./configmap.yaml)


# Secret

## Imperative

```bash
kubectl create secret generic <secret_name> --from-literal=<key>=<value>
kubectl create secret generic <secret_name> --from-file=<file_path>
```

## Declarative
[Example secret.yaml](./secret.yaml)


# Encrypting Data at Rest
https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/

Doing ```kubectl get secret <secret_name> -o yaml``` will show the data in base64 encoded format. You can decode it using ```echo <base64_encoded_string> | base64 --decode```.

We can create an EncryptionConfiguration file to encrypt the data at rest. The configuration file can be passed to the kube-apiserver using the ```--encryption-provider-config``` flag.

[Example EncryptionConfiguration file](./encryption_configuration.yaml)

After enabling --encryption-provider-config, every new secret will be encrypted. Previously created secrets will not be encrypted. To encrypt the existing secrets, we can use the following command:

```bash
kubectl get secret <secret_name> -o json | kubectl replace -f -
```
