# Building a Kubernetes Cluster with kubeadm

<img src="https://user-images.githubusercontent.com/6856382/221376352-df2dc8dc-0bbe-489d-bfc9-a4baeb1655fa.png">

## Loading Kernel Modules

1. the following lines of code are used to load modules typed thereafter to load on startup

**All Kubernetes Nodes**
```
cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay # Module number 1
br_netfilter # Module number 2
EOF
```

2. Load the kernel modules by typing in the following command
    - note 
        1. `sysctl` is used to manage system setting
        2. `modprobe` is used to load kernel modules 

**All Kubernetes Nodes**
```
sudo modprobe overlay
sudo modprobe br_netfilter
```

3. Set system configurations for Kubernetes networking
    - `tee` reads the standard input and writes it to both the standard output and one or more files

**All Kubernetes Nodes**
```
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF
```

4. Apply new setting
    - Note:
        1. `sudo sysctl -p` is used to reload kernel parameter values from configuration files
        2. `sudo sysctl --system` is used to reload all kernel parameters to their default value specified by the system
            - The author chose this because everything is set to default. It doesn't matter

**All Kubernetes Nodes**
```
sudo sysctl --system
```

5. Install `containerd`
    - More can be found [here](https://containerd.io/)

**All Kubernetes Nodes**
```
sudo apt-get update && sudo apt-get install -y containerd.io
```

6. Create default configuration file for containerd
    - **Note**:
        1. `\etc` folder contain all your system configuration files in it.

**All Kubernetes Nodes**
```
sudo mkdir -p /etc/containerd
```

7. Generate default containerd configuration and save to the newly created default file
    - `.toml` is a file format for configuration files

**All Kubernetes Nodes**
```
sudo containerd config default | sudo tee /etc/containerd/config.toml
```

8. Restart containerd to ensure new configuration file usage

**All Kubernetes Nodes**
```
sudo systemctl restart containerd
```

9. Verify that containerd is running:

**All Kubernetes Nodes**
```
sudo systemctl status containerd
```

10. Disable swap
    - **Why?**
        - Kubernetes requires the OS to disable swap

**All Kubernetes Nodes**
```
sudo swapoff -a
```

11. Install dependency packages (required for installation of kubernetes)

**All Kubernetes Nodes**
```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```

12. Download and add GPG key (for kubernetes)

**All Kubernetes Nodes**
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

13. Add Kubernetes to repository list

**All Kubernetes Nodes**
```
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

14. Update Package listing

**All Kubernetes Nodes**
```
sudo apt-get update
```

15. Install Kubernetes packages (Note: If you get a dpkg lock message, just wait a minute or two before trying the command again):

**All Kubernetes Nodes**
```
sudo apt-get install -y kubelet=1.24.0-00 kubeadm=1.24.0-00 kubectl=1.24.0-00
```

16. Turn off automatic updates

**All Kubernetes Nodes**
```
sudo apt-mark hold kubelet kubeadm kubectl
```

## Initialize the Cluster

1. On `Control Plane \ Kubernetes Master Node`, initialize the Kubernetes cluster on the control plane node using `kubeadm`

**Kubernetes Control Plane Node**
```
sudo kubeadm init --pod-network-cidr 192.168.0.0/16 --kubernetes-version 1.24.0
```

2. Set `kubectl` access

**Kubernetes Control Plane Node**
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

3. Test access to Cluster

**Kubernetes Control Plane Node**
```
kubectl get nodes
```

## Install the Calico Network Add-On

1. On the control plane node, install Calico Networking

**Kubernetes Control Plane Node**
```
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml
```

2. Check status of the control plane node

**Kubernetes Control Plane Node**
```
kubectl get nodes
```

## Join the Worker Nodes to the Cluster

1. In the control plane node, create the token and copy the `kubeadm join` command

```
kubeadm token create --print-join-command
```

2. Copy the full output from the previous command used in the control plane node. This command starts with `kubeadm join`

3. In both worker nodes, paste the full kubeadm join command to join the cluster. Use sudo to run it as root


**Kubernetes Worker Nodes** 
```
sudo kubeadm join
```

4. In the control plane node, view cluster status
    - it takes time to get to `Ready` status

**Kubernetes Control Plane**
```
kubectl get nodes
```

