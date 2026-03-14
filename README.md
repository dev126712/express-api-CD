````
.
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
│   ├── kustomization.yaml
│   └── namespace.yml
├── kustomization.yml
├── overlays
│   ├── dev
│   │   ├── backend
│   │   │   └── kustomization.yaml
│   │   ├── frontend
│   │   │   └── kustomization.yaml
│   │   └── kustomization.yaml
│   ├── production
│   │   ├── backend
│   │   │   └── kustomization.yaml
│   │   ├── frontend
│   │   │   └── kustomization.yaml
│   │   └── kustomization.yaml
│   └── staging
│       ├── backend
│       │   └── kustomization.yaml
│       ├── frontend
│       │   └── kustomization.yaml
│       └── kustomization.yaml
├── README.md
└── root.yml
````
