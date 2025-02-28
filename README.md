# Gitea on Kubernetes

Install Gitea on Kubernetes using [kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/), or just edit the files in `base/` before applying them.

# Deploy Gitea with kustomize | example

Create a `kustomization.yaml` and a `gitea-app.ini` file

```bash
# Create a kustomization.yaml file
cp kustomization-example.yaml kustomization.yaml

# Create a gitea-app.ini file
cp gitea-app-example.ini gitea-app.ini
```

Edit/Update `kustomization.yaml` and `gitea-app.ini`

To view the Deployment, run:

```bash
kustomize build .
# OR 
kubectl kustomize .
```

To apply/deploy, run:

```bash
kubectl kustomize . | kubectl apply -f -
#  OR
kubectl apply --kustomize .
```

ref: 
  * https://docs.gitea.com/administration/config-cheat-sheet
  * https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
