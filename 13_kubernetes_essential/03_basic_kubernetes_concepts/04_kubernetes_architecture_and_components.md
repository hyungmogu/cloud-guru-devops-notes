# Kubernetes Architecture and Components


<img src="https://user-images.githubusercontent.com/6856382/221396971-e9105176-e995-4c11-ace0-2eb5753b987b.png">

- Given the following list of pods

```
NAME                                                   READY   STATUS    RESTARTS   AGE
coredns-5d4dd4b4db-hhrq9                               1/1     Running   1          31h
coredns-5d4dd4b4db-jl8rb                               1/1     Running   1          31h
etcd-92c60ee3641c.mylabserver.com                      1/1     Running   4          31h
kube-apiserver-92c60ee3641c.mylabserver.com            1/1     Running   4          31h
kube-controller-manager-92c60ee3641c.mylabserver.com   1/1     Running   4          31h
kube-flannel-ds-amd64-84vpz                            1/1     Running   5          21h
kube-flannel-ds-amd64-95hj8                            1/1     Running   3          21h
kube-flannel-ds-amd64-ssjqp                            1/1     Running   4          21h
kube-proxy-4qrxs                                       1/1     Running   4          31h
kube-proxy-68545                                       1/1     Running   2          21h
kube-proxy-gbx79                                       1/1     Running   2          21h
kube-scheduler-92c60ee3641c.mylabserver.com            1/1     Running   4          31h
```

- kubernetes control plane is formed by:
    1. `etcd`, 
    2. `kube-apiserver`, 
    3. `kube-controller-manager`, 
    4. `kube-scheduler` 

## Etcd
- `etcd` provides distributed and synchronized data storage for the cluster state
- `etcd` is the distributed storage for the Kubernetes master server
- `etcd` contains all the information about
    1. What pods are running in the cluster
    2. What nodes are in the cluster
    3. All the different data objects that are part of the cluster


## Kube Apiserver
- `Kube-apiserver` serves the kubernetes api
- `kube-apiserver` serves in simple REST-based web api
- `kube-apiserver` is like front-facing interface (frontend)
- Example
    1. `kube-apiserver` is used anytime you are interacting with the cluster, including `kubectl`

## Kube Controller Manager
- `kube-controller-manager` has all the backend stuff
- `kube-controller-manager` does all the behind the scenes work of controlling the cluster

## Kube Scheduler
- `kube-scheduler` determines 
    1. when to run pods
    2. what nodes those pods need to run on
- `kube-scheduler` works behind the scene when
    1. you create a pod 
    2. you have a deployment
    3. automation of creating and destroying pods


## kubelet
- `kubelet` is not part of kubernetes control plane
- `kubelet` is part of individual nodes
- `kubelet` is the most important as non-control-plane component
- `kubelet` is an agent that runs on each node
- `kubelet` acts as a middleman between `kubernetes api` and container runtime (e.g. docker)
    - when container needs to be run on a node
        1. `kubelet` on the node is reached out by kubernetes control plane
        2. `kubelet` instructs container runtime to run the container

- `kubelet` is not a pod but is a service

```
sudo systemctl status kubelet
```

```
kubelet.service - kubelet: The Kubernetes Node Agent
   Loaded: loaded (/lib/systemd/system/kubelet.service; enabled; vendor prese
  Drop-In: /etc/systemd/system/kubelet.service.d
           └─10-kubeadm.conf
   Active: active (running) since Sun 2023-02-26 15:10:43 UTC; 1h 0min ago   
     Docs: https://kubernetes.io/docs/home/
 Main PID: 879 (kubelet)
    Tasks: 17 (limit: 2307)
   CGroup: /system.slice/kubelet.service
           └─879 /usr/bin/kubelet --bootstrap-kubeconfig=/etc/kubernetes/boot

...
```

## Kube Proxy

- `kube-proxy` exists in each node, including control plane
- `kube-proxy` handles networking such as
    1. network communication between different nodes
        - writes firewall rules to the routing tables of each node
        - e.g. a pod talking to another pod
        - e.g.2. routing traffic from one node to another node

