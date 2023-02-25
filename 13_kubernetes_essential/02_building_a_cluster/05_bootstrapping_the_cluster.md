# Bootstrapping the Cluster

- bootstrap means 

```
a technique of loading a program into a computer by means of a few initial instructions which enable the introduction of the rest of the program from an input device.
```

<img src="https://user-images.githubusercontent.com/6856382/221341978-241b765c-2775-44a5-8191-7cf7c351f137.png">

# Instruction

**Kubernetes Master**
```
# Initialize the cluster on the Kube Master server
sudo kubeadm init --pod-network-cidr=10.244.0.0/16

# Setup kubeconfig for the local user on the kube master server
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config  
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

**Kubernetes Nodes**
```
# copy paste the following code provided after `sudo kubeadm init`
[[sudo kubeadm join $controller_ip:6443 --token $token --discovery-token-ca-cert-hash $hash]]
```

**Kubernetes Master**
```
# verify that the kubernetes cluster is working correctly
kubectl get nodes
```

- After all this, it's expected to have `NOT READY` status

#