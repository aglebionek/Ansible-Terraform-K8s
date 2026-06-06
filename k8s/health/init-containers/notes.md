## Init Containers

### What are Init Containers?
- Special containers that run before the main application containers in a Pod start.
- Used for initialization tasks that need to be completed before the main containers can run, such as setting up the environment, waiting for a service to be available, or performing database migrations.
- Defined in the Pod specification under the `initContainers` field.

### Key Features of Init Containers
- Run sequentially: Each Init Container must complete successfully before the next one starts, and before the main application containers start.
- Can have different images and configurations than the main containers, allowing for specialized tasks.
- If an Init Container fails, Kubernetes will restart the Pod until it succeeds, ensuring that the initialization tasks are completed before the application runs.

### Example of Init Containers in a Pod Specification

