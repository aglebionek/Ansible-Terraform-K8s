# Namespaces
Namespaces allow separation of resources within a Kubernetes cluster.
They also allow to assign a resource quota to a namespace, which limits the amount of resources that can be used by the objects in that namespace.

<img src="./images/isolation.png" alt="isolation_diagram" width="600"/>

<img src="./images/resource_quota.png" alt="resource_quota_diagram" height="300"/>

Creating an object in cubernetes creates DNS entries for the object. If we want to access an object in the same namespace, we can simply use its name. If we want to access an object in a different namespace, we need to use its full name, which includes the namespace, the object name, and the cluster domain.

<img src="./images/dns.png" alt="dns_diagram" width="600"/>

<img src="./images/dns2.png" alt="dns2_diagram" width="600"/>

You can switch the default namespaces

<img src="./images/switch.png" alt="switch_diagram" width="800"/>
