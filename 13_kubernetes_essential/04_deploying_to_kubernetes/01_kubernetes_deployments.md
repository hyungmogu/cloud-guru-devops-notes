# Kubernetes Deployments

<img src="https://user-images.githubusercontent.com/6856382/221424690-b6d4d3db-0b43-4052-ab4a-daf7d2055211.png">

- this part is about how to deploy applications to kubernetes cluster

## Deployments

- `deployments` are a type of object in kubernetes
- `deployments` gives you more power to organize and maintain pods
- `deployments` is useful to start doing something more complex kubernetes project
- `deployments` allows the creation and management of pods
- `deployments` tell kubernetes cluster a `desired state` (what kubernetes cluster should look like)
    - kubernetes cluster constantly works in order to maintain the desired state

- `deployments` accomplishes the following:
    1. Scaling
    2. Rolling Updates
    3. Self-healing