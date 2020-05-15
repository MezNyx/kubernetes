Typical Install For Helm to Kustomize


First and foremost get helm installed and configured

helm url: helm.sh
helm github url: https://github.com/helm/helm/releases

Make sure to use Helm 3


Make sure Kubernetes is set up
Lots of info out there to do this. Not gonna document

Fetch the helm chart:
  - example: `helm fetch --untar --untardir charts hashicorp/vault`

Fetch the values:
  - example: `helm show values hashicorp/vault > values.yaml`

Template the chart:
  - example: `helm template vault --output-dir base --namespace vault --values values.yaml charts/vault`

Go to the base directory:
  - example: `cd base/vault`

Move all the files from templates to the cwd:
  - example: `mv templates/* . && rmdir templates`

Create a namespace yaml file:
  - example:
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: vault
```

Create your kustomization yaml file:
  - example:
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

Apply the folder:
  - example: `kubectl apply -k base/vault`
