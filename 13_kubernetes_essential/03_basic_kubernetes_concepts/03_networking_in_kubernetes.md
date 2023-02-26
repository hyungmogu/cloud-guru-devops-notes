# Networking in Kubernetes

<img src="https://user-images.githubusercontent.com/6856382/221389626-139bd225-9fcc-4ad5-8a44-efc0218ad442.png" />

1. `Kubernetes` creates a virtual network across the whole cluster
2. `Kubernetes` assigns a unique IP address for every pod in the cluster
3. `Kubernetes` can communicate with any pod in the cluster using this unique IP address, even if pod is running on a different node (server)
3. `Kubernetes` all in the cluster share single virtual network


## Flannel

1. `Flannel` is a plugin that creates this virtual network
2. `Flannel` allows pods to communicate with each other, regardless of which node they are on


## Example

- Create two pods

**Kubernetes Control Plane**
```
cat << EOF | kubectl create -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
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

2. check pods

```
kubectl get pods
```

3. Create third pod `busybox`

```
cat << EOF | kubectl create -f -
apiVersion: v1
kind: Pod
metadata:
  name: busybox
spec:
  containers:
  - name: busybox
    image: radial/busyboxplus:curl
    args:
    - sleep
    - "1000"
EOF
```

4. Check pods again in detail
    - Notice `busybox` and first `nginx` are running in the same server
    - the second `nginx` is running in different server

```
NAME                    READY   STATUS    RESTARTS   AGE     IP           NODE                           NOMINATED NODE   READINESS GATES
busybox                 1/1     Running   0          20s     10.244.1.4   92c60ee3642c.mylabserver.com   <none>           <none>
nginx-9b644dcd5-974h6   1/1     Running   0          2m31s   10.244.1.3   92c60ee3642c.mylabserver.com   <none>           <none>
nginx-9b644dcd5-wvct7   1/1     Running   0          2m31s   10.244.2.4   92c60ee3643c.mylabserver.com   <none>           <none>
```

#