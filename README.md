# Three-Tier Architecture Deployment ( Kustomize ) With External Database

![alt text](https://github.com/dev126712/express-api-CD/blob/341a5c49ff3a99e73eed880e7d385d3715318225/Screenshot%202026-03-29%201.12.43%20PM.png)

Kustomize structure:
````
.
├── argocd
│   ├── argocd-dev.yml
│   ├── argocd-prod.yml
│   └── argocd-stage.yml
├── base
│   ├── backend
│   │   ├── backend-configmap.yml
│   │   ├── backend-deployment.yml
│   │   ├── backend-hpa.yml
│   │   ├── backend-secrets.yml
│   │   ├── backend-serivice.yml
│   │   └── kustomization.yaml
│   ├── frontend
│   │   ├── frontend-configmap.yml
│   │   ├── frontend-deploymeny.yml
│   │   ├── frontend-hpa.yml
│   │   ├── frontend-service.yml
│   │   └── kustomization.yaml
│   └── kustomization.yaml
├── kustomization-dev
│   └── kustomization.yml
├── kustomization-prod
│   └── kustomization.yml
├── kustomization-stage
│   └── kustomization.yml
├── overlays
│   ├── dev
│   │   ├── backend
│   │   │   └── kustomization.yaml
│   │   ├── frontend
│   │   │   ├── default.conf.template
│   │   │   └── kustomization.yaml
│   │   ├── kustomization.yaml
│   │   └── namespace.yml
│   ├── production
│   │   ├── backend
│   │   │   └── kustomization.yaml
│   │   ├── frontend
│   │   │   └── kustomization.yaml
│   │   ├── kustomization.yaml
│   │   └── namespace.yml
│   └── staging
│       ├── backend
│       │   └── kustomization.yaml
│       ├── frontend
│       │   └── kustomization.yaml
│       ├── kustomization.yaml
│       └── namespace.yml
├── README.md
````

