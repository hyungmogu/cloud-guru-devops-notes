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
#