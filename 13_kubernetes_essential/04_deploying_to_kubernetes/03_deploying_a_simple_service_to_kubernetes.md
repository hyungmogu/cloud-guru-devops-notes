# Deploying a Simple Service to Kubernetes

## Instruction

1. Create the deployment with four replicas (provided)

**Kubernetes Control Plane**
```
cat << EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: store-products
  labels:
    app: store-products
spec:
  replicas: 4
  selector:
    matchLabels:
      app: store-products
  template:
    metadata:
      labels:
        app: store-products
    spec:
      containers:
      - name: store-products
        image: linuxacademycontent/store-products:1.0.0
        ports:
        - containerPort: 80
EOF
```

2. Make sure that deployment is successful

**Kubernetes Control Plane**
```
kubectl get deployments
```

```
NAME             DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
store-products   4         4         4            4           4m14s
```

3. Create a `store-product-service` and verify that you can access it from the busybox testing pod (already provided)

**Kubernetes Control Plane**

```
cat << EOF | kubectl apply -f -
kind: Service
apiVersion: v1
metadata:
  name: store-products
spec:
  selector:
    app: store-products
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
EOF
```

4. Check that service is up in the cluster

**Kubernetes Control Plane**
```
kubectl get services
```

or 

```
kubectl get svc
```

```
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP   173m
store-products   ClusterIP   10.103.53.88   <none>        80/TCP    8m39s
```

5. Query the store-products service from busybox testing pod

```
kubectl exec busybox -- curl -s store-products
```

```
{
        "Products":[
                {
                        "Name":"Apple",
                        "Price":1000.00,
                },
                {
                        "Name":"Banana",
                        "Price":5.00,
                },
                {
                        "Name":"Orange",
                        "Price":1.00,
                },
                {
                        "Name":"Pear",
                        "Price":0.50,
                }
        ]
}
```

