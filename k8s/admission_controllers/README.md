# Admission controllers
Admission controllers are plugins that govern and enforce how the cluster is used. They can be used to validate requests to the Kubernetes API server, mutate objects before they are persisted, or even reject requests based on custom logic.

<img src="./images/example.png" alt="example_diagram" width="600"/>

List of admission controllers
```bash
kubectl exec kube-apiserver -n kube-system -- kube-apiserver -h | grep enable-admission-plugins
#
kube-apiserver -h
```

## Changing admission plugins

You can edit the kube-apiserver manifest file to enable or disable admission controllers. The manifest file is usually located at `/etc/kubernetes/manifests/kube-apiserver.yaml` on the master node.

Flags for admission controllers
```bash
--enable-admission-plugins=<admission_controller_1>,<admission_controller_2>,...
--disable-admission-plugins=<admission_controller_1>,<admission_controller_2>,...
```

Flag for custom admission controllers. NOTE: This path has to be mounted to the kube-apiserver container in order for the admission controller to be able to read it.
```bash
--admission-control-config-file=<path_to_config_file>
```

## Custom admission webhooks
We can run a custom admission webhook server, with custom code and logic, to validate or mutate the requests to the Kubernetes API server.
The webhook server will receive an AdmissionReview object, with the "request" field containing all the details of the request made to the K8S API server.

We can basically separate the admission controllers into two types: validating and mutating.
That's why K8S gives us two custom admission webhook types: ValidatingAdmissionWebhook and MutatingAdmissionWebhook.
The webhook server returns an AdmissionReview object, with the "response" field containing the result of the admission check (request.uuid and allowed/denied decision).

[Validating Admission Webhook Example](./validating_admission_webhook.yaml)
