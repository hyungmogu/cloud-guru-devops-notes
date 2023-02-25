# Building a Kubernetes Cluster with kubeadm

<img src="https://user-images.githubusercontent.com/6856382/221376352-df2dc8dc-0bbe-489d-bfc9-a4baeb1655fa.png">

## Loading Kernel Modules

1. the following lines of code are used to load modules typed thereafter to load on startup

```
cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
```

**Example**

```
cat << EOF | sudo tee /etc/modules-load.d/containerd.conf
> overlay # Module number 1
> br_netfilter # Module number 2
> EOF
```

