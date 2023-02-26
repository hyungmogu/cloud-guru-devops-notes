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

## CMD - kubectl create service
- `kubectl create service <service_name>` creates a service on top of chosen pods

**Kubernetes Control Plane**
```

```

## Example - Creating Service on top of the two pods

#