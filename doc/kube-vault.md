### Single Instance Vault Server

## Port Fordward to Vault
```Shell
kubectl port-forward vault-0 8200:8200
```

## Initialize Vault
```Shell
kubectl exec -it vault-0 --namespace vault -- vault operator init -n 1 -t 1
```

## Unseal Vault
```Shell
kubectl exec -it vault-0 --namespace vault -- vault operator unseal ${InitialRootToken}
```

### HA Vault Cluster

## Get Vault Pods
```Shell
kubectl get pods -l app.kubernetes.io/name=vault
```

## Initialize Vault
```Shell
kubectl exec -ti vault-0 -- vault operator init
```

## Unseal Vault
```Shell
## Unseal the first vault server until it reaches the key threshold
kubectl exec -ti vault-0 -- vault operator unseal # ... Unseal Key 1
kubectl exec -ti vault-0 -- vault operator unseal # ... Unseal Key 2
kubectl exec -ti vault-0 -- vault operator unseal # ... Unseal Key 3
```

Repeat the unseal process for all Vault pods. When all Vault server pods are unsealed they report READY 1/1

```Shell
kubectl get pods -l app.kubernetes.io/name=vault
NAME                                    READY   STATUS    RESTARTS   AGE
vault-0                                 1/1     Running   0          1m49s
vault-1                                 1/1     Running   0          1m49s
vault-2                                 1/1     Running   0          1m49s
```

