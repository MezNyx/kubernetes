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
kubectl port-forward service/$servicename --namespace $namespace $local_port:$remote_port
```

### Quickly help troubleshoot pod issues
```Shell
kubectl describe pod $pod_name | grep -A 3 Events
```
