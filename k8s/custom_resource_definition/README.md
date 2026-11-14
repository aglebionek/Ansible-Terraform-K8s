# Custom Resource Definition (CRD)
In K8S, you can create custom objects that are not part of the default K8S API.

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: flightickets.flights.com # <names.plural>.<group>
spec:
  scope: Namespaced
  group: flights.com # GROUP
  names:
    kind: Flighticket # KIND
    plural: flightickets
    singular: flighticket
    shortNames:
      - ft
  versions:
    - name: v1 # VERSION
      served: true # Is served by the API server?
      storage: true # Is this version used to store the object in etcd?
      schema: # The spec of the object
        openAPIV3Schema:
          type: object
          properties:
            spec: # SPEC
              type: object
              properties: 
                destination:
                  type: string
                origin:
                  type: string
                numberOfSeats:
                  type: integer
                  minimum: 1
                  maximum: 10

---
apiVersion: flights.com/v1 # GROUP/VERSION
kind: Flighticket # KIND
metadata:
  name: flighticket-1
spec: #SPEC
  destination: "New York"
  origin: "Los Angeles"
  numberOfSeats: 5
```

The above example creates a flight ticket CRD. We can now use regular kubectl commands to create, read, update, and delete flight ticket objects.
However, the Flightticket object is currently not really doing anything. At this point, it's just a data structure in the ETCD database.
To make the Flightticker object actually do something, we need to create a custom controller.

# Custom Controller
A custom controller is a program that watches for changes to the Flighticket objects and takes action based on those changes.
To create one, we use the kubernetes golang library.
We can start with this [example repo](https://github.com/kubernetes/sample-controller).

One we create and build our custom controller, we can put it into a Docker image and run it as a pod in our K8S cluster.

However, that would mean each time we setup a new cluster, we would have to deploy our custom controller pod and create the CRD.
To avoid this, we can use the Operator framework.

# Operator Framework
The Operator framework allows us to package our custom controller and CRD into a single deployable unit called an Operator.
