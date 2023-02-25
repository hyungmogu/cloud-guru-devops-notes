# Building a Kubernetes Cluster with kubeadm

<img src="https://user-images.githubusercontent.com/6856382/221376352-df2dc8dc-0bbe-489d-bfc9-a4baeb1655fa.png">

## Loading Kernel Modules

1. the following lines of code are used to load modules typed thereafter to load on startup

**Master Kubernetes Node**
```
cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
> overlay # Module number 1
> br_netfilter # Module number 2
> EOF
```

2. Load the kernel modules by typing in the following command
    - note 
        1. `sysctl` is used to manage system setting
        2. `modprobe` is used to load kernel modules 

**Master Kubernetes Node**
```
sudo modprobe overlay
sudo modprobe br_netfilter
```

3. Set system configurations for Kubernetes networking
    - `tee` reads the standard input and writes it to both the standard output and one or more files

**Master Kubernetes Node**
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

```
sudo sysctl --system
```

