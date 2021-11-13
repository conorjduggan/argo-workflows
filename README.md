# argo-workflows

Based off of https://argoproj.github.io/argo-workflows/quick-start/

## Prerequisites 
* Minikube is running.
    * `minikube start`

## Deploying using Helm
You can deploy this project 2 different ways.

### Deploying directly from the inside the project
1. Deploy the Helm chart.
    * `helm install argo-worklflows argo-worklflows`

### Packaging the project and unstalling the tar file
1. We need to be outside the repo before we run these commands.
    * `cd ..`
2. Package the Helm chart.
    * `helm package argo-worklflows`
3. Deploy the Helm chart.
    * `helm install argo-worklflows argo-worklflows`

## Deploying using kubectl

### Install argocd into Minikube
1. Create the argocd namespace.
    * `kubectl apply -f templates/namespace.yaml`
2. Deploy argocd into the namespace.
    * `kubectl apply -n argo-worklflows -f templates/argo-install.yaml`

### Expose the argocd UI
`kubectl -n argo port-forward deployment/argo-server 2746:2746`

## Deploy a sample workflow
```
argo submit -n argo --watch https://raw.githubusercontent.com/argoproj/argo-workflows/master/examples/hello-world.yaml
argo list -n argo
argo get -n argo @latest
argo logs -n argo @latest
```