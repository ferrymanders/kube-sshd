# kube-sshd
Templates for running an ssh daemon in kubernetes for the purpose of port-forwarding

## Setup
Create a configmap with your public ssh key.
```
kubectl create configmap ssh-keys --from-file /path/to/.ssh/authorized_keys
```

Create pod
```
kubectl create -f https://raw.githubusercontent.com/ferrymanders/kube-sshd/main/configmap-sshd-config.yaml
kubectl create -f https://raw.githubusercontent.com/ferrymanders/kube-sshd/main/pod-sshd.yaml
```

## Connect to container
Setup port-forward.
```
kubectl port-forward pod/sshd 2222
```

SSH into pod, username is configurable in pod template.
```
ssh -p 2222 user@localhost
```

Create a port-forward to a hostname further in cluster
```
ssh -p 2222 user@localhost -L 8443:my-service.my-namespace.svc.cluster.local:443 -N
```