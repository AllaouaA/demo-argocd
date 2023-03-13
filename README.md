#### Commands

```bash
# set proxy
export https_proxy=http://10.101.30.8:3128

# install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f argocd-install/install.yaml

# check pods status
kubectl get po -n argocd -w

# access ArgoCD UI
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# login with admin user and below token (as in documentation):
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password
#Generating a bcrypt hash for the password: https://www.browserling.com/tools/bcrypt (test)
# bcrypt(password)=$2a$10$PwPtsXd6Cl9MSdQ2KiIG.upmIT2ObMTmZsI8/gW33PJZz553IkPTW
# enocde bcrypt(password)=JDJhJDEwJFB3UHRzWGQ2Q2w5TVNkUTJLaUlHLnVwbUlUMk9iTVRtWnNJOC9nVzMzUEpaejU1M0lrUFRX
kubectl -n argocd patch secret argocd-secret  -p '{"data": {"admin.password": "JDJhJDEwJFB3UHRzWGQ2Q2w5TVNkUTJLaUlHLnVwbUlUMk9iTVRtWnNJOC9nVzMzUEpaejU1M0lrUFRX", "admin.passwordMtime": ""}}'
kubectl -n argocd scale deployment argocd-server --replicas=0
kubectl -n argocd scale deployment argocd-server --replicas=1

# create azureth secret
kubectl create secret docker-registry azureth --docker-server=https://seiitraregistrytp.azurecr.io --docker-username=6b7a8136-0e40-4b7f-866c-9de992a54f44 --docker-password=hK88Q~GmI1avHXgJgFYqKrYXlCi~wEwC7GGYhcGA -n $ns
 
```
</br>

#### Links


* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)