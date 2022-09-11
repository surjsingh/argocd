# argocd



## Installation

Install regular or ha or core setup

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
argocd app create \
--name helm-guestbook \
--project demo \
--repo https://github.com/surjsingh/argocd.git \
--dest-server https://kubernetes.default.svc \
--dest-namespace helm-guestbook \
--path helm-guestbook

argocd app list
argocd app get helm-guestbook
argocd app sync helm-guestbook
argocd app history helm-guestbook
argocd app delete helm-guestbook
```

CLI Install

```
curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.1.5/argocd-linux-amd64
chmod +x /usr/local/bin/argocd

argocd login localhost:8080 --insecure
```
