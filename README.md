# Kubernetes Demo Application

This repository contains Kubernetes manifests for deploying a demo application using ArgoCD.

## Files

- `deployment.yaml`: Kubernetes Deployment manifest for the demo application
- `service.yaml`: Kubernetes Service manifest for exposing the demo application
- `argocd-application.yaml`: ArgoCD Application manifest for deploying the application

## Deployment Instructions

### Prerequisites

- Kubernetes cluster (e.g., kind, minikube, EKS)
- ArgoCD installed in the cluster
- kubectl configured to access the cluster

### Deploy with kubectl

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Deploy with ArgoCD

1. First, update the `argocd-application.yaml` file to point to your repository:
   ```yaml
   spec:
     source:
       repoURL: https://github.com/YOUR_USERNAME/k8s-demo-app.git
   ```

2. Apply the ArgoCD Application manifest:
   ```bash
   kubectl apply -f argocd-application.yaml
   ```

3. ArgoCD will automatically sync and deploy the application.

## Accessing the Application

The application is exposed as a NodePort service on port 30080. You can access it at:

```
http://<node-ip>:30080
```

For local development with kind or minikube, you can use port-forwarding:

```bash
kubectl port-forward svc/demo-app-service 8080:80
```

Then access the application at http://localhost:8080
