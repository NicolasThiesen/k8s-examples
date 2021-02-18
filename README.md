# K8S example

## Pre-requisites
- You must to pre intalled docker and kubernetes
- You must already deployed nginx ingress contreller
## To run

- Build the docker images

```shell
docker build Cat-Website -t local/cat-website
docker build Monkey-Website -t local/monkey-website
docker build Main-Page -t local/mainpage
```
- Push into your repository
- Update your repo on `image:` in deployment.yaml file
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