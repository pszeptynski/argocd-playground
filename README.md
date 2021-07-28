# argocd-playground

1. Deploy Argo CD
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. Create the NodePort service for ArgoCD server by using:

```
kubectl apply -f argocd-server-nodeport.yaml
```

3. Apply application CRD for Nginx manifests.

```
kubectl apply -f argocd-crd-nxing.yaml
```

