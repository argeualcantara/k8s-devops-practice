# Kubernetes Practice with MiniKube

## Install minikube

Follow the instructions in this link
https://minikube.sigs.k8s.io/docs/start/

Create an alias for minikube kubectl:

```bash
alias mk="minikube kubectl --"
```


## Install Metal LB

https://metallb.universe.tf/installation/

MetalLB will act as a public ip provider, like the cloud providers.

Change the values in the kube-proxy configmap in kube-system namespace:

```yaml
mode: "ipvs"
ipvs:
  strictARP: true
```

Next we will install te metal lb in our cluster

```bash
mk apply -f metalLB/metallb.yaml
```

and we need to create a secret for metal lb

```bash
mk create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
```

## Install Nginx Ingress controller

https://kubernetes.github.io/ingress-nginx/deploy/

## Deploy echoserver