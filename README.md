# Kubernetes Demo

Requirements: Docker, kubectl, minikube

### Minikube Setup

```sh
minikube start
```

```sh
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

Access the application:

```sh
# Option 1: "NodePort"
kubectl expose deployment kubernetes-bootcamp --type="NodePort" --port 8080
kubectl port-forward svc/kubernetes-bootcamp 8080:8080
curl localhost:8080

# Option 2: "LoadBalancer"
kubectl expose deployment kubernetes-bootcamp --type='LoadBalancer' --port=8080
minikube tunnel
curl localhost:8080
```

