## Useful Kubernetes Commands and Cheat Sheet


### Re-init a new bootstrap tocken
```bash
sudo kubeadm init phase bootstrap-token
```

### Get the sha256 hash for joining
```bash
openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
```

### Get new join command with new token
```bash
kubeadm token create --print-join-command
```

### Port Forwarding
```bash
kubectl port-forward service/$servicename --namespace $namespace $local_port:$remote_port
```

### Quickly help troubleshoot pod issues
```bash
kubectl describe pod $pod_name | grep -A 3 Events
```
