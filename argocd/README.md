# Argo CD ApplicationSet for pingpong-gitops-config

This directory contains an `AppProject` and a single `ApplicationSet` that generates Applications
for each combination of service (`ping`, `pong`) and environment (`dev`, `qa`, `preprod`, `prod`).

## Requirements
- Argo CD is installed and running in the `argocd` namespace.
- The ApplicationSet controller is installed (usually part of standard Argo CD Helm charts or install manifests).

## Repo URL
Configured to deploy from: `https://github.com/daoquocquyen/pingpong-gitops-config.git`

## What gets generated
The ApplicationSet creates Applications named `<service>-<env>` such as `ping-dev`, `pong-prod`.
Each Application points to the corresponding Kustomize overlay at `<service>/overlays/<env>` and deploys to the namespace `<service>-<env>`.
`CreateNamespace=true` is enabled so target namespaces are created if they don't exist.

## Bootstrap
Apply the project and the ApplicationSet:

```bash
kubectl apply -f argocd/project.yaml
kubectl apply -f argocd/appset.yaml
```

Argo CD will reconcile and generate the 8 Applications automatically.
