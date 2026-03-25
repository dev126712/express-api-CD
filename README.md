Kustomize structure:
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
│   └── kustomization.yaml
├── overlays
│   ├── dev
│   │   ├── backend
│   │   │   └── kustomization.yaml
│   │   ├── frontend
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
├── kustomization.yml (overlays/dev/)
├── README.md
└── root.yml
````


CI Pipeline (Security):

````

┌───────────────────────────────────────┬────────────┬───────────────────┐
│                Target                 │    Type    │ Misconfigurations │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/backend/backend-configmap.yml    │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/backend/backend-deployment.yml   │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/backend/backend-hpa.yml          │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/backend/backend-secrets.yml      │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/backend/backend-serivice.yml     │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/frontend/frontend-configmap.yml  │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/frontend/frontend-deploymeny.yml │ kubernetes │         2         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/frontend/frontend-hpa.yml        │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/frontend/frontend-service.yml    │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ base/namespace.yml                    │ kubernetes │         0         │
├───────────────────────────────────────┼────────────┼───────────────────┤
│ root.yml                              │ kubernetes │         0         │
└───────────────────────────────────────┴────────────┴───────────────────┘



Tests: 24 (SUCCESSES: 22, FAILURES: 2)
Failures: 2 (HIGH: 2, CRITICAL: 0)

KSV-0014 (HIGH): Container 'frontend' of Deployment 'frontend' should set 'securityContext.readOnlyRootFilesystem' to true
════════════════════════════════════════
An immutable root file system prevents applications from writing to their local disk. This can limit intrusions, as attackers will not be able to tamper with the file system or write foreign executables to disk.

See https://avd.aquasec.com/misconfig/ksv-0014
────────────────────────────────────────
 base/frontend/frontend-deploymeny.yml:17-36
────────────────────────────────────────
  17 ┌       - name: frontend
  18 │         image: dev126712/express-client:v4.0.7
  19 │         envFrom:
  20 │         - configMapRef:
  21 │             name: frontend-config
  22 │         ports:
  23 │         - containerPort: 5173
  24 │         resources:
  25 └           requests:
  ..   
────────────────────────────────────────


KSV-0118 (HIGH): deployment frontend in express-ns namespace is using the default security context, which allows root privileges
════════════════════════════════════════
Security context controls the allocation of security parameters for the pod/container/volume, ensuring the appropriate level of protection. Relying on default security context may expose vulnerabilities to potential attacks that rely on privileged access.

See https://avd.aquasec.com/misconfig/ksv-0118
────────────────────────────────────────
 base/frontend/frontend-deploymeny.yml:15-36
────────────────────────────────────────
  15 ┌     spec:
  16 │       containers:
  17 │       - name: frontend
  18 │         image: dev126712/express-client:v4.0.7
  19 │         envFrom:
  20 │         - configMapRef:
  21 │             name: frontend-config
  22 │         ports:
  23 └         - containerPort: 5173
  ..   
────────────────────────────────────────

````
