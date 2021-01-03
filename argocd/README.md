# Argo CD


## Installation


## Configure Applications

### Configure Helm Charts

```
|--- Chart.yaml
|--- templates
|    |--- stuff.yaml
|    |--- stuff-dependency.yaml
|--- values.yaml
```

### Configure App

```
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: <insert helm chart here>
  namespace: argocd
  finalizers:
    - resources-finalizer.argocd.argoproj.io
spec:
  destination:
    namespace: <insert namespace here>
    server: https://kubernetes.default.svc
  project: default
  source:
    helm:
      releaseName: k8s
      valueFiles:
        - values.yaml
    path: helm/<patth>/<to>/<values>
    repoURL: https://github.com/foo/kubernetes.git
    targetRevision: main
  syncPolicy:
    automated:
      selfHeal: true
      prune: true
```


### Information
https://argoproj.github.io/argo-cd/operator-manual/cluster-bootstrapping/
