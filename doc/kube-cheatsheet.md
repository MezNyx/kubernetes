## Useful Kubernetes Commands and Cheat Sheet


### Re-init a new bootstrap tocken
```Shell
sudo kubeadm init phase bootstrap-token
```

### Get the sha256 hash for joining
```Shell
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```

### Get new join command with new token
```Shell
kubeadm token create --print-join-command
```

### Port Forwarding
```Shell
kubectl port-forward service/${servicename} --namespace ${namespace} ${local_port}:${remote_port}
```

### Quickly help troubleshoot pod issues
```Shell
kubectl describe pod ${pod} | grep -A 3 Events
```

### Find which nodes a pod is running on
```Shell
kubectl get pod -o=custom-columns=Name:.metadata.name,STATUS:.status.phase,NODE:.spec.nodeName
```

## Kubernetes Plugins

### Krew
```Shell
(
  set -x; cd "$(mktemp -d)" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.{tar.gz,yaml}" &&
  tar zxvf krew.tar.gz &&
  KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" &&
  "$KREW" install --manifest=krew.yaml --archive=krew.tar.gz &&
  "$KREW" update
)
```
```Shell
echo 'export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"' >> ${HOME}/.zshrc
```

### ctx and ns
```Shell
kubectl krew install ctx
kubectl krew install ns
kubectl ns
  default
  kube-node-lease
  kube-public
  kube-system

kubectl ctx
  user-context@cluster
  kubernetes-admin@kubernetes
```
