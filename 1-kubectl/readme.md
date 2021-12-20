# Simple K8S Deployment Tutorial with kubectl

## Layer of Abstraction
Everything below Deployment is managed by Kubernetes
- Deployment manages a ReplicaSet
- ReplicaSet manages a Pod
- Pod is an abstraction of Container

## Create Deployments
Create nginx deploment
```sh
kubectl create deployment nginx-depl --image=nginx
```
Create mongo deployment
```sh
kubectl create deployment mongo-depl --image=mongo
```
Show running services
```sh
kubectl get deployment
kubectl get replicaset
kubectl get pod
```

## Port Forward Nginx Deployment
Create nginx deploment
```sh
kubectl port-forward deployment/nginx-depl 8080:80
```

## Edit Running Deployment
Edit deployment Nginx image to nginx:1.16
```sh
kubectl edit deployment <deployment-name>
```

## Show Pod logs
```sh
kubectl logs <pod-name>
```

## Show detailed info
```sh
kubectl describe <pod-name>
```

## Accessing Into Pod
```sh
kubectl exec -it <pod-name> -- bin/bash
```
## Delete Deployment
```sh
kubectl delete deployment <deployment-name>
```
## Configure K8S declaratively using file yaml
```sh
kubectl apply -f filename.yaml
```