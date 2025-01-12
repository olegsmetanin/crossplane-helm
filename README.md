# Crossplane helm provider example

1. Install K8s, configure KUBECONFIG
2. Install Crossplane
```
helm repo add crossplane https://charts.crossplane.io/stable
helm upgrade --install --create-namespace -n crossplane-system --version="1.18.1" crossplane crossplane/crossplane
```
3. Install ArgoCD
```
helm repo add argocd https://argoproj.github.io/argo-helm
helm upgrade --install --create-namespace -n argo-cd --version="7.7.7" argo-cd argocd/argo-cd
```
4. Get ArgoCD admin password
```
kubectl -n argo-cd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
5. Port-forward ArgoCD
```
kubectl port-forward service/argo-cd-argocd-server -n argo-cd 8080:443
```
6. Open http://localhost:8080 and accept the certificate, login to ArgoCD
7. Create API Access token in github
8. Configure repository and project in ArgoCD for helm-chart deployment from this repository using access token
9. Sync deployment in ArgoCD, check deployment status of nginx
10. Port-forward nginx
```
kubectl port-forward service/nginx-example -n nginx-example 8081:80
```
11. Check nginx workload, open http://localhost:8081
