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

```
NAMESPACE     NAME                                         
          READY   STATUS              RESTARTS   AGE       
default       nginx                                        
          0/1     ContainerCreating   0          3m1s      

...

kube-system   kube-flannel-ds-amd64-84vpz                  
          1/1     Running             1          7h22m     
kube-system   kube-flannel-ds-amd64-95hj8                  
          1/1     Running             2          7h22m     
kube-system   kube-flannel-ds-amd64-ssjqp                  
          1/1     Running             2          7h22m     
kube-system   kube-proxy-4qrxs                             
          1/1     Running             2          18h       
kube-system   kube-proxy-68545                             
          1/1     Running             1          7h52m     
kube-system   kube-proxy-gbx79                             
          1/1     Running             1          7h51m     
```


## kubectl describe pod
1. `kubectl describe pod <POD_NAME>` is useful for troubleshooting an existing / deployed pod



```
Name:         nginx
Namespace:    default
Priority:     0
Node:         92c60ee3642c.mylabserver.com/172.31.22.94
Start Time:   Sun, 26 Feb 2023 01:33:11 +0000
Labels:       <none>
Annotations:  <none>
Status:       Running
IP:           10.244.1.2
Containers:
  nginx:
    ...
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-vphm7:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-vphm7
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s  
                 
Events:
  Type     Reason                  Age                  From              
                     Message
  ----     ------                  ----                 ----              
                     -------
  Normal   Scheduled               8m13s                default-scheduler                      
  Normal   Pulling                 38s                  kubelet, 92c60ee3642c.mylabserver.com  Pulling image "nginx"
  Normal   Pulled                  34s                  kubelet, 92c60ee3642c.mylabserver.com  Successfully pulled image "nginx"
  Normal   Created                 33s                  kubelet, 92c60ee3642c.mylabserver.com  Created container nginx
  Normal   Started                 33s                  kubelet, 92c60ee3642c.mylabserver.com  Started container nginx
```

#