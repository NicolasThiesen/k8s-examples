# K8S example

## Pre-requisites
- You must to pre intalled docker and kubernetes
- You must already deployed nginx ingress contreller
## To run

- First step create namespaces:

```shell
kubectl create namespace cat
kubectl create namespace monkey
kubectl create namespace mainpage
```

- Build the docker images

```shell
docker build Cat-Website -t local/cat-website
docker build Monkey-Website -t local/monkey-website
docker build Main-Page -t local/mainpage
```

- Create a deployment

```shell
kubectl apply -f deployment.yaml
```

- Create a service

```shell
kubectl apply -f service.yaml
```

- Create a ingress

```shell
kubectl apply -f ingress.yaml
```