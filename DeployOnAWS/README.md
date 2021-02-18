# Deploy on AWS

## Prerequisites

- kubectl
- eksctl
- helm

## Steps

- Deploy the cluster

```shell
eksctl create cluster --name my-cluster --region us-east-1 --zones us-east-1c,us-east-1d --with-oidc --ssh-access --ssh-public-key worldskill-lap --managed -t t2.medium
```

- Create the iam policy for the Load Balancer Controller

```shell
aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json

```

- Create a IAM role and ServiceAccount

```shell

eksctl create iamserviceaccount --cluster my-cluster --namespace kube-system --name aws-load-balancer-controller --attach-policy-arn arn:aws:iam::${ACCOUNT_ID}:policy/AWSLoadBalancerControllerIAMPolicy --override-existing-serviceaccounts --approve
```

- Install the TargetGroupBinding CRDs

```shell
kubectl apply -k github.com/aws/eks-charts/stable/aws-load-balancer-controller/crds?ref=master

kubectl get crd
```

- Add de eks-charts repository on helm

```shell
helm repo add eks https://aws.github.io/eks-charts
```

- Deploy the Helm chart

```shell
helm upgrade -i aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=my-cluster --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set image.tag="v2.0.0"

kubectl -n kube-system rollout status deployment aws-load-balancer-controller
```