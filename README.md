# Gitea on Kubernetes

Install Gitea on Kubernetes using [kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/), or just copy `gitea.yml` and edit it before applying it

# Deploy Gitea with kustomize | example

Create a `kustomization.yaml` and a `ingress-patch.yaml` file

```bash
# Create a kustomization.yaml file
cat <<EOF >./kustomization.yaml
namespace: gitea

bases:
  - https://github.com/jefferyb/k8s-gitea.git?ref=v1.0.0

commonLabels:
  app: gitea
  env: production

patchesJson6902:
  - path: ingress-patch.yaml
    target:
      group: extensions
      version: v1beta1
      kind: Ingress
      name: gitea
EOF

# Create a ingress-patch.yaml file
cat <<EOF >./ingress-patch.yaml
- op: replace
  path: /spec/rules/0/host
  value: gitea.192.168.1.37.nip.io
EOF

```

To view the Deployment, run:

```bash
kubectl kustomize ./
```

To apply/deploy, run:

```bash
kubectl kustomize ./ | kubectl apply -f -
#  OR
kubectl apply --kustomize ./
```

ref: 
  * https://github.com/go-gitea/gitea/blob/v1.13.0-dev/contrib/k8s/gitea.yml
  * https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
