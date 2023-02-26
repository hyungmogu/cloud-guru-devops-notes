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

