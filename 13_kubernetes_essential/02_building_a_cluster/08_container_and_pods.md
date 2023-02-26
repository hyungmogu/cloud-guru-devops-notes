# Container and Pods

<img src="https://user-images.githubusercontent.com/6856382/221383843-47ed7691-9dba-4290-8c80-a5f32bc0bf76.png"/>

## Pods

1. Pods are the smallest and most basic building block of the Kubernetes model
    - Pod is required to run a container in kubernetes cluster 

2. Pod can have more than 1 container
    - Usually pod has 1 container


## Scheduling

1. is a process of running container on individual nodes
    - Kubernetes schedules pods to run on specific servers in order to run containers

## Kubectl

- Before applying `kubectl create -f`, apply the following command to install necessary modules

**All Nodes**
```
wget https://github.com/containernetworking/plugins/releases/download/v0.8.6/cni-plugins-linux-amd64-v0.8.6.tgz
sudo tar -C /opt/cni/bin -xzvf cni-plugins-linux-amd64-v0.8.6.tgz
sudo systemctl restart kubelet
```

- `kubectl create -f <yml file name>` is used to create a pod

**Kubernetes Control Plane**
```
cat << EOF | kubectl create -f -
apiVersion: v1
kind: Pod
metadata:
    name: nginx
spec:
    containers:
    - name: nginx
      image: nginx
EOF
```

- `kubectl get pods` is used to get all ponds
    - `-n` flag is used to define specific name space
    - default name space is used if none given

**Kubernentes Control Plane**
```
kubectl get pods -n kube-system
```

or

```
kubectl get pods

```

or

```
kubectl get pods --all-namespaces
```


## kubectl describe pod
1. `kubectl describe pod <POD_NAME>` is useful for troubleshooting an existing / deployed pod

#