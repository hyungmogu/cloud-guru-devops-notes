# Clustering and Nodes

<img src="https://user-images.githubusercontent.com/6856382/221388388-22f5ae73-bf80-4b8e-bac1-dbdc069e1b60.png"/>

## Kubernetes Cluster

- `Kubernetes cluster` have multiple servers that are able to run our containers
- `Kubernetes cluster` is not just dependent on 1 individual machine
- `Kubernetes Cluster` are spread across a variety of multiple different servers

## Kubernetes Nodes
- `Kubernetes node` is a server which actually run containers
- There are two different types of servers in a `Kubernetes Cluster`
    1. Control Server 
        - Manages and controls the cluster
        - Hosts the Kubernetes API
        - Can be multiple (for high availability)
        - Usually separate from worker nodes
    2. Worker nodes
        - Responsible for running actual application workloads

<img src="https://user-images.githubusercontent.com/6856382/221388607-71fe48ff-227c-439c-b8b8-2a36f13cc162.png" />

## kubectl describe node

- `kubectl describe node <node_name>` can be used to gain detailed information about a node
    - `Allocated Resources` section is one of useful section (describes resource usage)

**Kubernetes Control Plane**
```
kubectl describe node 92c60ee3641c.mylabserver.com
```

```
Name:               92c60ee3641c.mylabserver.com
Roles:              master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=92c60ee3641c.mylabserver.com
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/master=        
Annotations:        flannel.alpha.coreos.com/backend-data: {"VtepMAC":"ce:fc:e9:ca:db:28"}
                    flannel.alpha.coreos.com/backend-type: vxlan
                    flannel.alpha.coreos.com/kube-subnet-manager: true
                    flannel.alpha.coreos.com/public-ip: 172.31.30.68
                    kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0        
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 25 Feb 2023 07:25:34 +0000        
Taints:             node-role.kubernetes.io/master:NoSchedule
Unschedulable:      false
Conditions:
  Type             Status  LastHeartbeatTime               
  LastTransitionTime                Reason                 
      Message
  ----             ------  -----------------               
  ------------------                ------                 
      -------
  MemoryPressure   False   Sun, 26 Feb 2023 02:17:55 +0000   Sat, 25 Feb 2023 07:25:30 +0000   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Sun, 26 Feb 2023 02:17:55 +0000   Sat, 25 Feb 2023 07:25:30 +0000   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Sun, 26 Feb 2023 02:17:55 +0000   Sat, 25 Feb 2023 07:25:30 +0000   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Sun, 26 Feb 2023 02:17:55 +0000   Sun, 26 Feb 2023 01:40:43 +0000   KubeletReady           
      kubelet is posting ready status. AppArmor enabled    
Addresses:
  InternalIP:  172.31.30.68
  Hostname:    92c60ee3641c.mylabserver.com
Capacity:
 cpu:                2
 ephemeral-storage:  20252352Ki
 hugepages-1Gi:      0
 hugepages-2Mi:      0
 memory:             1998448Ki
 pods:               110
Allocatable:
 cpu:                2
 ephemeral-storage:  18664567573
 hugepages-1Gi:      0
 hugepages-2Mi:      0
 memory:             1896048Ki
 pods:               110
System Info:
 Machine ID:                 9ef2866073d1434aa3bdbde3f2f26eb1
 System UUID:                ec215a8d-9201-bf23-add1-796669f3bed7
 Boot ID:                    99ab2be5-0a8b-4c68-86d8-fffabfadb491
 Kernel Version:             5.4.0-1096-aws
 OS Image:                   Ubuntu 18.04.6 LTS
 Operating System:           linux
 Architecture:               amd64
 Container Runtime Version:  docker://18.6.1
 Kubelet Version:            v1.15.7
 Kube-Proxy Version:         v1.15.7
PodCIDR:                     10.244.0.0/24
Non-terminated Pods:         (6 in total)
  Namespace                  Name                          
                          CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
  ---------                  ----                          
                          ------------  ----------  ---------------  -------------  ---
  kube-system                etcd-92c60ee3641c.mylabserver.com                       0 (0%)        0 (0%)      0 (0%)           0 (0%)         18h
  kube-system                kube-apiserver-92c60ee3641c.mylabserver.com             250m (12%)    0 (0%)      0 (0%)           0 (0%)         18h
  kube-system                kube-controller-manager-92c60ee3641c.mylabserver.com    200m (10%)    0 (0%)      0 (0%)           0 (0%)         18h
  kube-system                kube-flannel-ds-amd64-84vpz                             100m (5%)     0 (0%)      50Mi (2%)        0 (0%)         8h
  kube-system                kube-proxy-4qrxs              
                          0 (0%)        0 (0%)      0 (0%)           0 (0%)         18h
  kube-system                kube-scheduler-92c60ee3641c.mylabserver.com             100m (5%)     0 (0%)      0 (0%)           0 (0%)         18h
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                650m (32%)  0 (0%)
  memory             50Mi (2%)   0 (0%)
  ephemeral-storage  0 (0%)      0 (0%)
Events:
  Type    Reason                   Age   From              
                     Message
  ----    ------                   ----  ----              
                     -------
  Normal  Starting                 37m   kubelet, 92c60ee3641c.mylabserver.com  Starting kubelet.
  Normal  NodeHasSufficientMemory  37m   kubelet, 92c60ee3641c.mylabserver.com  Node 92c60ee3641c.mylabserver.com status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    37m   kubelet, 92c60ee3641c.mylabserver.com  Node 92c60ee3641c.mylabserver.com status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     37m   kubelet, 92c60ee3641c.mylabserver.com  Node 92c60ee3641c.mylabserver.com status is now: NodeHasSufficientPID
  Normal  NodeNotReady             37m   kubelet, 92c60ee3641c.mylabserver.com  Node 92c60ee3641c.mylabserver.com status is now: NodeNotReady
  Normal  NodeAllocatableEnforced  37m   kubelet, 92c60ee3641c.mylabserver.com  Updated Node Allocatable limit across pods
  Normal  NodeReady                37m   kubelet, 92c60ee3641c.mylabserver.com  Node 92c60ee3641c.mylabserver.com status is now: NodeReady
```

