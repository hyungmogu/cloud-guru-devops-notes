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
mkdir -p $HOME/kube
sudo cp -i /etc/kubernetes/admin.confg $HOME/.kube/config
sudo chown $(id -u) $HOME/.kube/config
```

#