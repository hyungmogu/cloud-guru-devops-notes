# Kubernetes Services


<img src="https://user-images.githubusercontent.com/6856382/221437262-8db08035-c156-40db-bd9d-81f2977ada7f.png">

- `kubernetes services` is important component of deploying applications to a Kubernetes cluster

## Services
- `services` allows to dynamically access a group of replica pods
- `services` acts like an abstraction layer on top of a set of pods
    - like a load balancer
- `services` are useful in following cases:
    1. How to access specific, but changing pod if there is something external to the cluster that needs communication?

- `services` is done by
    1. providing load balanced usage of dynamic list of pods
        - making request to `kubernetes services` gives response from 1 of the pods that is part of the service
        - making request to `kubenetes services` is always routed to 1 of the active pods  

## CMD - kubectl get svc
- `kubectl get svc` returns list of services
- `kubectl get svc` is the same as `kubectl get service`

**Kubernetes Control Plane**
```
kubectl get svc
```

```
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP        38h
nginx-service   NodePort    10.101.71.138   <none>        80:30080/TCP   50s
```

## Example - Creating Service on top of the two pods

1. Create Kubernetes Service
    - `selector` is really important
        - determines which pod makes up the service
    - `nodePort` allows to expose the service externally
        - listens on all nodes
        - routes to kubernetes service if anything extneral communicates with any of 3 servers on the port  
        - routes the traffic to 1 of pods connected to `service`
        - not always the best way to communicate

```
cat << EOF | kubectl create -f -
kind: Service
apiVersion: v1
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
  type: NodePort
EOF
```

2. Make a request and see if one of nginx pods responds

**Kubernetes Control Plane**
```
curl localhost:30080
```

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;   
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to    
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

#