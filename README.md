# argo demo

1. Install ArgoCD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

2. Install argo workflows

```
kubectl create ns argo
kubectl apply -n argo -f https://raw.githubusercontent.com/argoproj/argo-workflows/stable/manifests/namespace-install.yaml
```

3. Give proper access rights 

```
kubectl create rolebinding default-admin --clusterrole=admin --serviceaccount=argo:default --namespace=argo
kubectl create clusterrolebinding argo-server-clusterworkflows --clusterrole=admin --serviceaccount=argo:argo-server -n argo
```

4. Patch config

```
kubectl patch configmap/workflow-controller-configmap \
  -n argo \
  --type merge \
  -p '{"data":{"containerRuntimeExecutor":"pns"}}'
```
