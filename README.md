# argocd
My ArgoCD Configuration


# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# access ArgoCD UI
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# Helm Way
helm repo add argo https://argoproj.github.io/argo-helm
helm install argo argo/argo-cd --version 5.20.4 --namespace argocd --create-namespace
kubectl port-forward  svc/argo-argocd-server 8080:443 -n argocd


## login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

## Apply configuration
kubectl apply -f ./argocd


 ### minikube configuration
minikube addons enable default-storageclass
minikube addons enable storage-provisioner
minikube addons enable ingress
echo "$(minikube ip) minikube" | sudo tee -a /etc/hosts

###
kubectl -n logging get secret elasticsearch-master-credentials -o jsonpath="{.data.password}" | base64 --decode && echo
kubectl -n logging get secret elasticsearch-master-credentials -o jsonpath="{.data.username}" | base64 --decode && echo