# argocd-playground

Just a short info without all the details. More here: https://argo-cd.readthedocs.io/en/stable/getting_started/

## Part I. Humble beginnings.

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
kubectl get app -n argocd
```

4. Log in to Argo CD web UI (get your IP address and port number from file at 2.). Click your app, click Sync and see all the blows and whistles in graphical form. Play with filters to see more details.
5. Check what's going on in the console, because why would Argo lie:

```
kubectl get deploy -n nginx-demo
kubectl get svc -n nginx-demo
kubectl get cm -n nginx-demo
```

## Part II. Helm to the rescue.

1. Created some Helm charts and stuff. Now let's pull them into Argo CD and create staging env.

```
kubectl apply -f argocd-crd-helm-nginx-staging.yaml
```

2. The new app called nginx-staging should appear in Argo CD web UI. Click it and click Sync. See the magic you've seen before. One pod with nginx-alpine is created as we stated in values-staging.yaml

3. Check in the console:

```
kubectl get ns
kubectl get deployment -n nginx-helm-staging
kubectl get svc -n nginx-helm-staging
kubectl get cm -n nginx-helm-staging
kubectl get cm -n nginx-helm-staging -o yaml | grep "version:"
```

4. Repeat the steps and deploy the Helm chart for prod env.

```
kubectl apply -f argocd-crd-helm-nginx-prod.yaml
```

5. Nginx-prod app should appear in Argo CD web UI. This time with two pods after sync according to parameters in values-prod.yaml.
6. Check in console with commands as in 3. using `nginx-helm-prod` as namespace.


