## Cluster Setup v1.30

### Master Node
```bash
$ sudo hostnamectl set-hostname master.example.com
$ exec bash 
```
### Worker Node-1
```bash
$ sudo hostnamectl set-hostname worker-node-1.example.com
$ exec bash
```

### Worker Node-2
```bash
$ sudo hostnamectl set-hostname worker-node-2.example.com
$ exec bash
```

### Master Node Initialization
```bash
$ sudo kubeadm init
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
- Install Container Network Interface (CNI) 
```bash
$ kubectl delete -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml

$ kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml
```
- Verification
```bash
$ kubectl get nodes
```
- Get the join command for the worker nodes
```bash
sudo kubeadm token create --print-join-command ## Copy and save the command
```
### Worker Nodes initialization
#### Worker Node - 1
- Execute the Join command 
```bash
$ sudo kubeadm join 172.31.42.226:6443 --token yenoeb.xpx0wiewbgezrt0d --discovery-token-ca-cert-hash sha256:a99cc7b66034de3b5a7a14d5e6effce758b71071b58a9871786315bc2026be06 ## example here.
``` 

#### Worker Node - 2
- Execute the Join command 
```bash
$ sudo kubeadm join 172.31.42.226:6443 --token yenoeb.xpx0wiewbgezrt0d --discovery-token-ca-cert-hash sha256:a99cc7b66034de3b5a7a14d5e6effce758b71071b58a9871786315bc2026be06 ## example here.
```

### Check from the master node
```bash
$ kubectl get nodes
```

### Basic Command of Kubectl
```bash
$ kubectl get nodes
$ kubectl get nodes -o wide
$ kubectl describe node worker-node-1.example.com
```

### Deploying the first pod and accessing it
```bash
$ kubectl run nginxpod --image=nginx --port 80
$ kubectl get pods
$ kubectl describe pod nginxpod
$ kubectl exec -it nginxpod /bin/sh
$ kubectl logs nginxpod
```


