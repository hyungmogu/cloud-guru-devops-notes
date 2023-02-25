# Installing Kubeadm, Kubelet, Kubectl

<img src="https://user-images.githubusercontent.com/6856382/221334390-a542a4f3-9967-46dc-a934-ee0a12ca3142.png">

## Kubeadm

- `kubeadm` makes the construction of kubernetes cluster much much easier

## Kubelet

- `kubelet` is an essential part of kubernetes
- `kubelet` is an agent in each node
- `kubelet` handles running containers on a node
- `kubelet` serves as a middleman between docker and kubernetes API
    - tells docker 
        1. when to setup container, and 
        2. when to teardown container
- `kubelet` manages each individual node

## Kubectl

- `kubectl` is for managing and using clusters

## Installing Kubeadm, Kubelet, and Kubectl
- Must be done to both master, and all worker nodes
- More for recent version can be found [here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)


**For Tutorial Version**
```
# Add Kubernetes Repository GPG key
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

# Add Kubernetes Repository
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

# Reload the apt sources list
sudo apt-get update

# Install packages
sudo apt-get install -y kubelet=1.15.7-00 kubeadm=1.15.7-00 kubectl=1.15.7-00

# Hold auto upgrading of kubeadm, kubectl, kubelet
sudo apt-mark hold kubelet kubeadm kubectl

# Check version
kubeadm version
```

#