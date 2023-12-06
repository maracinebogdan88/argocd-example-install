Code for blog post: https://www.arthurkoziel.com/setting-up-argocd-with-helm/

``` 
helm repo add argo-cd https://argoproj.github.io/argo-helm
helm dep update charts/argo-cd/
echo "charts/**/charts" >> .gitignore
helm install argo-cd charts/argo-cd/
kubectl get pods
kubectl port-forward svc/argo-cd-argocd-server 8080:443
kubectl get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
helm template root-app/ | kubectl apply -f -
``` 