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