# Setup Kubernetes Kind

## Create Kind Cluster
```sh
kind create cluster --config  kind-node-cluster.yaml
```

## Delete Kind Cluster
```sh
kind delete cluster
```

## Setup Metallb Load Balancer
1. Create the metallb namespace 
    ```sh
    kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/master/manifests/namespace.yaml
    ```
2. Create the memberlist secrets
    ```sh
    kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)" 
    ```
3. Apply metallb manifest
    ```sh
    kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/master/manifests/metallb.yaml
    ```
    
## Setup Metallb Load Balancer Address Pool
1. Get docker kind network IP range
    ```sh
    docker network inspect -f '{{.IPAM.Config}}' kind
    ```
2. Setup address pool config map based on CIDR kind network IP range, adjust "addresses" value inside metallib-configmap.yaml

3. Apply address poll config map
    ```sh
    kubectl apply -f metallb-configmap.yaml
    ```