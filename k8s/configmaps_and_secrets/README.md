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
