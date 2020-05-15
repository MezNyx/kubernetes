## Typical Install For Helm to Kustomize


### Install Helm 3

- helm url: [helm.sh](https://helm.sh)
- helm github url: [helm releases](https://github.com/helm/helm/releases)


### Create Kustomized Deployment

- Fetch the helm chart: `helm fetch --untar --untardir charts hashicorp/vault`
- Fetch the values: `helm show values hashicorp/vault > values.yaml`
- Template the chart: `helm template vault --output-dir base --namespace vault --values values.yaml charts/vault`
- Move all the files from templates for cleanliness: `mv base/vault/templates/* base/vault/ && rmdir templates`
- Create a namespace yaml file:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: vault
```

- Create your kustomization yaml file:
```bash
ls -1 # copy the filenames
vi kustomization.yaml
```

```yaml
namespace: vault
resources:
  - injector-clusterrolebinding.yaml
  - injector-clusterrole.yaml
  - injector-deployment.yaml
  - injector-mutating-webhook.yaml
  - injector-serviceaccount.yaml
  - injector-service.yaml
  - namespace.yaml
  - server-clusterrolebinding.yaml
  - server-config-configmap.yaml
  - server-headless-service.yaml
  - server-serviceaccount.yaml
  - server-service.yaml
  - server-statefulset.yaml
  - volumes.yaml
```

- Apply the folder: `kubectl apply -k base/vault`
