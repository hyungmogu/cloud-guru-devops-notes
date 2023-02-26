# Kubernetes Deployments

<img src="https://user-images.githubusercontent.com/6856382/221424690-b6d4d3db-0b43-4052-ab4a-daf7d2055211.png">

- this part is about how to deploy applications to kubernetes cluster

## Deployments

- `deployments` gives you more power to organize and maintain pods
- `deployments` is useful to start doing something more complex kubernetes project
- `deployments` tell kubernetes cluster a `desired state` (what kubernetes cluster should look like)
    - kubernetes cluster constantly works in order to maintain the desired state

- `deployments` accomplishes the following:
    1. Scaling
        - is done by specifying the number of replicas
        - is done by making sure replicas are evenly spread across multiple nodes for high availability 
    2. Rolling Updates
        - is a mean of deploying new versions of application 
        - is done by gradually rolling out new pods and replacing old pods
            - reduces downtime
    3. Self-healing
        - is done by immediately creating a new pod and replace the damaged / missing one
        - is done to maintain the `desired state`

## Example of Deployment

- Create two replicas

**Kubernetes Control Plane**

```
cat <<EOF | kubectl create -f -apiVersion: apps/v1
kind: Deployment
metadata: 
name: nginx-deployment  
labels: 
app: nginx 
spec: 
replicas: 2  
selector: 
matchLabels: 
app: nginx  
template: 
metadata: 
labels: 
app: nginx  
spec:
containers: 
- name: nginx
image: nginx:1.15.4 
ports:
- containerPort: 80
EOF
```

## CMD - kubectl get deployments
- `kubectl get deployments` is used to get information about list of deployments

**Kubernetes Control Plane**
```
kubectl get deployments
```

```
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
nginx   2/2     2            2           16h
```

## CMD - kubectl describe deployment
- `kubectl describe deployment <deployment_name>` is used to attain details about a deployment

**Kubernetes Control Plane**
```
kubectl describe deployment nginx
```

```
Name:                   nginx
Namespace:              default
CreationTimestamp:      Sun, 26 Feb 2023 02:59:06 +0000    
Labels:                 app=nginx
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge 
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx:1.15.4
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-9b644dcd5 (2/2 replicas created)    
Events:          <none>
```