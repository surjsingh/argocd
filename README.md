# argocd



## Installation

Install full or core components

```
kubectl create ns argocd
kubectl apply -f install/install.yaml #fullversion
kubectl apply -f install/core-install.yaml #onlycorecomponents
kubectl port-forward svc/argocd-server -n argocd 8080:443
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
Login to `https://localhost:8080` with username as `admin` and temp admin password from the above secret

Next, create an example app in argocd to deploy your application via manifest or alternatively via argocd commandline
`kubectl create ns helm-guestbook`

```
kubectl apply -f apps/helm-guestbook.yaml
or
argocd app create --name helm-guestbook \
--repo https://github.com/surjsingh/argocd.git \
--dest-server https://kubernetes.default.svc \
--dest-namespace helm-guestbook --path helm-guestbook
```
