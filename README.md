# pingpong-config

Declarative Kubernetes manifests for the **ping/pong** demo, using Kustomize.
This repo is designed for GitOps tools (e.g., Argo CD or Flux) and follows a per-service base + environment overlays layout.

## Structure
- `ping/` and `pong/`: each service has its own `base/` (Deployment + Service) and `overlays/` for environments.
- Environments: `pingpong-dev`, `pingpong-qa`, `pingpong-preprod`, `pingpong-prod` (namespace per environment).

## Apply locally (example: dev)
```bash
kubectl apply -k ping/overlays/dev
kubectl apply -k pong/overlays/dev
```

## Promotion
Promote by updating the `images.newTag` in the target overlay, open a PR, and let your GitOps controller sync.
