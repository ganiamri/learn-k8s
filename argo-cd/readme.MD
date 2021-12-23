# Setup ArgoCD

## Install ArgoCD
1. Create ArgoCD Namespace
    ```sh
    kubectl create namespace argocd
    ```
2. Default ArgoCD Installation - Official Docs
    ```sh
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    ```
    Enhance ArgoCD Installation - CoreDNS Issue ndots
    ```sh
    kubectl apply -n argocd -f argocd.yaml
    ```
## Accessing ArgoCD Web App
Service Type Load Balancer
```sh
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```
Ingress
```sh
https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/
```
Port Forwarding
```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
## Get Admin Password
Login Using The CLI
```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
## Install First ArgoCD Application
```sh
kubectl apply application.yaml
```