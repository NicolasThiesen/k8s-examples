# K8S example

## Prerequisites
- You must to intalled docker.
- You must to intalled kubernetes ( kubectl is enough ).
- You must to installed eksctl.
- You must to installed helm.
- You must already deployed [the cluster on AWS](https://github.com/NicolasThiesen/k8s-examples/tree/master/DeployOnAWS).
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
