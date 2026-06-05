K8s will restart your container on probe failure, app crashes, container process exiting, etc. The restart policy is defined in the pod spec, and it can be one of the following:
- Always (default) - always restart the container if it fails
- OnFailure - restart the container only if it fails with a non-zero exit code
- Never - never restart the container, even if it fails