# Configuring Networking with Flannel

<img src="https://user-images.githubusercontent.com/6856382/221372271-8e60f34b-192d-48e7-b6a1-3b9f7b907b92.png">

## Setting up Flannel

1. `net.bridge-bridge-nf-call-iptables` must be turned on for the networking to work
    - Please do this to:
        1. Master node
        2. All Worker nodes
    - `| sudo tee -a /etc/sysctl.conf` Allows the value to apply even after computer restarts

**To All Nodes**
```
# set value `net.bridge.bridge-nf-call-iptables=1`, and make it apply even after computer restarts
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf

# Make configuration to apply immediately
sudo sysctl -p
```

2. `kubectl apply` is used in `Kubernetes Master` node to install flannel on all nodes
    - `kubectl apply` would apply some kind of configuration to the clusters
    - `-f` means file

**Kubernentes Master Node**
```
# Install Flannel in the cluster by running this only on the Master node:
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel-old.yaml
```

3. Verify that all the nodes now have Status of `Ready`
    - It's now working because networking is installed and setup

**Kubernetes Master Node**
```
kubectl get nodes
```

```
NAME                           STATUS   ROLES    AGE   VERSION
f8bbdd78c31c.mylabserver.com   Ready    master   15m   v1.15.7
f8bbdd78c32c.mylabserver.com   Ready    <none>   12m   v1.15.7
f8bbdd78c33c.mylabserver.com   Ready    <none>   12m   v1.15.7
```

4. Verify that the Flannel pods are up and running
    - Should find three (in this case) with `flannel` in name
    - All the pods with `flannel` should have a status of `RUNNING`

**Kubernetes Master Node**
```
kubectl get pods -n kube-system
```

```
NAME                                                   READY   STATUS              RESTARTS   AGE
coredns-5d4dd4b4db-hhrq9                               0/1     ContainerCreating   0          10h
coredns-5d4dd4b4db-jl8rb                               0/1     ContainerCreating   0          10h
etcd-92c60ee3641c.mylabserver.com                      1/1     Running             1          10h
kube-apiserver-92c60ee3641c.mylabserver.com            1/1     Running             1          10h
kube-controller-manager-92c60ee3641c.mylabserver.com   1/1     Running             1          10h
kube-flannel-ds-amd64-84vpz                            1/1     Running             0          3m31s #This guy
kube-flannel-ds-amd64-95hj8                            1/1     Running             0          3m31s #This guy
kube-flannel-ds-amd64-ssjqp                            1/1     Running             0          3m31s #This guy
kube-proxy-4qrxs                                       1/1     Running             1          10h
kube-proxy-68545                                       1/1     Running             0          33m
kube-proxy-gbx79                                       1/1     Running             0          32m
kube-scheduler-92c60ee3641c.mylabserver.com            1/1     Running             1          10h
```