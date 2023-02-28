# Deploying a Microservice Application to Kubernetes (important)

## Steps

1. clone the repo that contains the pre-made descriptions

**kubernetes control plane**
```
git clone https://github.com/linuxacademy/robot-shop.git
```

2. Since this application has many components, it is a good idea to create a separate namespace for the app

**kubernetes control plane**
```
kubectl create namespace robot-shop
```

3. Deploy app to the cluster

**kubernetes control plane**
```
kubectl -n robot-shop create -f ~/robot-shop/K8s/descriptors
```

4. Check the status of the application's pods

**kubernetes control plane**
```
kubectl get deployments -n robot-shop
```

4. check if the app is alive by accessing the app using the Kube master node's public IP

**To Browser**
```
http://$kube_master_public_ip:30080
```

<img src="https://user-images.githubusercontent.com/6856382/221887582-8edbe4c1-fcb6-45a6-8289-4d1be1349ea9.png">

## Scale up the MongoDB deployment to two replicas instead of just one

1. Edit the deployment descriptor

**kubernetes control plane**
```
kubectl edit deployment mongodb -n robot-shop
```

2. You should see some YAML describing the deployment object.
    - Under `spec:` look for the line that says `replicas: 1` and change it to `replicas: 2`
    - save and exit

<img src="https://user-images.githubusercontent.com/6856382/221887040-90e15116-73da-45b1-85e7-83b579360fb0.png">

3. Check the status of the deployment with

```
kubectl get deployment mongodb -n robot-shop
```

<img src="https://user-images.githubusercontent.com/6856382/221888705-ef2196cc-4050-4c17-bfc6-767dfb9fc9da.png">

## CMD - kubectl edit

- `kubectl edit deployment <deployment_name> -n <cluster_name>` allows to scale up or scale down specific pods in a kubernetes cluster

```
kubectl edit deployment mongodb -n robot-shop
```

