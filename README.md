# Kubernetes Demo

Requirements: Docker, kubectl, minikube

### Minikube Setup

```sh
minikube start
```

```sh
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

### External Access

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

### Labeling

```sh
kubectl label $(kubectl get pods -o name) version=v1
```

### Scaling

```sh
# scale up
kubectl scale deployments/kubernetes-bootcamp --replicas=4

# scale down
kubectl scale deployments/kubernetes-bootcamp --replicas=2
```

### Rolling Updates

```sh
# updating to v2
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2
# confirming rollout status
kubectl rollout status deployments/kubernetes-bootcamp

# updating failed image v10
kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10
# undo the rollout
kubectl rollout undo deployments/kubernetes-bootcamp
# sanity check
kubectl get deploy -o wide
```