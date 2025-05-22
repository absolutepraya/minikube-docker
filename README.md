# Reflection on Hello Minikube

## 1. Comparing application logs before and after exposing as a Service

Before exposing the Deployment as a Service, the application logs display the server startup messages (e.g., HTTP server listening on port 8080, UDP server on port 8081) but no incoming request logs. After running `minikube service hellonode` and opening the app multiple times in the browser, each HTTP request generates a new log entry in the container logs. With each refresh, the number of log entries increases, confirming that each request is recorded independently.

![](./images/1.png)

## 2. Purpose of the `-n` option in `kubectl get` and why custom resources were not listed

The `-n` (or `--namespace`) option tells `kubectl` to list or operate on resources within a specific Kubernetes namespace. By default, resources are listed from the `default` namespace—where our `hellonode` Deployment and Service reside. When running `kubectl get pods,services -n kube-system`, the command switches to the `kube-system` namespace context and therefore does not show the `hellonode` resources, as they are not located in `kube-system` but in the `default` namespace.
