ArgoCD installing in kubernetes.
All of this based on official instalation instructions
kreate namespace: kubectl create namespace argocd
add cerificats
kubectl -n argocd create secret tls kube-ca-secret \
--cert=/etc/kubernetes/pki/ca.crt \
--key=/etc/kubernetes/pki/ca.key
installing cermanager
https://cert-manager.io/docs/installation/
installing ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
We need to change server.insecure: "true" so kubectl -n agrocd apply -f argocd-cmd-params-cm.yaml
Exposing with Ingress Controller
kubectl apply -f argocd-server-http-ingress.yaml
checking admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d ; echo
