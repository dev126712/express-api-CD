# Express API — Kubernetes Delivery (Kustomize + ArgoCD)

GitOps continuous delivery for the [Express API / SubTracker](https://github.com/dev126712/express-api) platform. Kustomize base/overlay structure with ArgoCD applications for three environments.

[![My Skills](https://skillicons.dev/icons?i=kubernetes,docker)](https://skillicons.dev)

![ArgoCD](https://github.com/dev126712/express-api-CD/blob/341a5c49ff3a99e73eed880e7d385d3715318225/Screenshot%202026-03-29%201.12.43%20PM.png)

---

## GitOps Flow

```
express-api repo (app code CI)
    │  image tag updated
    ▼
express-api-CD repo (this repo)
    │  ArgoCD watches
    ▼
GKE Cluster  ←  express-api-Infrastructure (Terraform)
```

---

## Kustomize Structure

```
base/                          # Shared manifests for all environments
├── backend/
│   ├── backend-deployment.yml
│   ├── backend-configmap.yml
│   ├── backend-hpa.yml
│   ├── backend-secrets.yml
│   ├── backend-service.yml
│   └── kustomization.yaml
└── frontend/
    ├── frontend-deployment.yml
    ├── frontend-configmap.yml
    ├── frontend-hpa.yml
    ├── frontend-service.yml
    └── kustomization.yaml

overlays/
├── dev/           # Namespace: dev   — lower resource limits, 1 replica
├── staging/       # Namespace: stage — mid-tier resources
└── production/    # Namespace: prod  — full replicas, prod configs

argocd/
├── argocd-dev.yml
├── argocd-prod.yml
└── argocd-stage.yml
```

Each overlay patches only what changes per environment (image tag, replica count, resource limits, ingress host). The base is never duplicated.

---

## Deploy

Apply the ArgoCD Application for a target environment:

```bash
# Dev
kubectl apply -f argocd/argocd-dev.yml

# Staging
kubectl apply -f argocd/argocd-stage.yml

# Production
kubectl apply -f argocd/argocd-prod.yml
```

ArgoCD watches this repo and auto-syncs on every push to `main`.

---

## Related Repos

| Repo | Role |
|---|---|
| [express-api](https://github.com/dev126712/express-api) | Application code + DevSecOps CI |
| [express-api-Infrastructure](https://github.com/dev126712/express-api-Infrastructure) | Terraform GKE cluster + ArgoCD + API Gateway |
