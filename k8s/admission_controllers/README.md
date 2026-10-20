# Admission controllers
Admission controllers are plugins that govern and enforce how the cluster is used. They can be used to validate requests to the Kubernetes API server, mutate objects before they are persisted, or even reject requests based on custom logic.

<img src="./images/example.png" alt="example_diagram" width="600"/>

List of admission controllers
```bash
kubectl exec kube-apiserver -n kube-system -- kube-apiserver -h | grep enable-admission-plugins
#
kube-apiserver -h
```

Flags for admission controllers
```bash
--enable-admission-plugins=<admission_controller_1>,<admission_controller_2>,...
--disable-admission-plugins=<admission_controller_1>,<admission_controller_2>,...
```
