# Monitoring solutions for Kubernetes clusters
K8s does not come with a built-in monitoring solution. However, there are many third-party solutions available that can be used to monitor Kubernetes clusters. Some popular options include:
- Metrics Server: A lightweight, short-term, in-memory monitoring solution that collects resource metrics from the kubelet and exposes them via the Kubernetes API. 
- Prometheus: A powerful, open-source monitoring and alerting toolkit that can be used to collect and store metrics from Kubernetes clusters. It can be integrated with Grafana for visualization.
- Elastic Stack: A collection of open-source tools (Elasticsearch, Logstash, and Kibana) that can be used to collect, store, and visualize logs and metrics from Kubernetes clusters.

## Metrics Server
Metrics Server is a cluster-wide aggregator of resource usage data. It collects metrics from the kubelet using the cAdvisor API and exposes them via the Kubernetes API. Metrics Server is designed to be lightweight and efficient, making it suitable for use in production environments.

### Deploy
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

### Use
```bash
kubectl top nodes
kubectl top pods
```

# Logs
```bash
kubectl logs -f <pod_name> -c <container_name>
```
-f follows the log output
-c specifies the container name if the pod has multiple containers