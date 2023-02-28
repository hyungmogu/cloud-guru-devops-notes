# Deploying Robot Shop App

<img src="https://user-images.githubusercontent.com/6856382/221486726-3bb3c8b9-77c3-49d6-8627-f369ed2ec7cf.png">

- `Kubernetes Descriptors` allow easy setup of microservices application involving many components
- `Kubernetes Descriptors` are a collection of yaml files

## Steps

1. clone the following github repo containing ready-made YAML files that can be used to quickly and easily install the application
    - `/K8s/descriptors` has all the files needed to setup and service the microserivce application

```
https://github.com/linuxacademy/robot-shop
```

<img src="https://user-images.githubusercontent.com/6856382/221770601-01d1ddaa-edec-46c9-aa71-bb1e845b4036.png">


2. Create Namespace for the kubernetes cluster and deploy resources
    - This is to make sure the parts fall under the same group

```
kubectl create namespace robot-shop
kubectl -n robot-shop create -f <path_where_k8s_descriptors_files_are>
```

<img src="https://user-images.githubusercontent.com/6856382/221775203-6754f7cd-872c-40cc-917a-8c6f64ef1c3e.png">

3. Check deployment
- add `-w` flag to watch changes made to the list on real time basis

```
kubectl get pods -n robot-shop -w
```

<img src="https://user-images.githubusercontent.com/6856382/221776988-3b5804e4-ee42-4bf1-b82c-153a02d1ba31.png">

4. 

#