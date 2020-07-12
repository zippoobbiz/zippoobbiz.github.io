---
title: local k8s sandbox for fun
date: 2020-07-12 13:00:20
tags: [kubernetes, minikube, istio, rancher, helm, vault, consul]
---


Run an internal vault inside k8s using consul as the backend.
Use k8s auth backend, retrieve secrets using service accout.

# Minikube

- `minikube config set driver virtualbox`       set the driver
- `minikube delete`                             delete the existing cluster
- `minikube start --memory=16384 --cpus=4 --kubernetes-version=v1.17.5` Request enough memory and cpu for istio, can use later version of k8s version

# Istio

## install
- `curl -sL https://istio.io/downloadIstioctl | sh -`  install CLI
- `export PATH=$PATH:$HOME/.istioctl/bin`

## init
- `kctx` -- make sure the context is pointing to minikube
- `istioctl operator init`

# Rancher
- `docker run -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher`

# helm
## install
- `brew install helm`
Or
- `curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3`
- `chmod 700 get_helm.sh`
- `./get_helm.sh`

## deploy vault 
- `helm search repo hashicorp/vault`
- `helm repo add hashicorp https://helm.releases.hashicorp.com`
```yaml
global:
  datacenter: vault-kubernetes-guide

client:
  enabled: true

server:
  replicas: 1
  bootstrapExpect: 1
  disruptionBudget:
    maxUnavailable: 0
```
- `helm install consul hashicorp/consul --values helm-consul-values.yml`
```yaml
server:
  affinity: ""
  ha:
    enabled: true
```
- `helm install vault hashicorp/vault --values helm-vault-values.yml`