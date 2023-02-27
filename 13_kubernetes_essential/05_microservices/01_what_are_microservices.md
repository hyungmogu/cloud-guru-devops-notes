# What are Microservices

<img src="https://user-images.githubusercontent.com/6856382/221466513-8a60207a-0ae6-4d70-855b-4dfb7211f79a.png">

1. `Microservices` is the area where Kubernetes really shines

## Microserivces

- `Microservices` are an application architecture
- `Microservices` means building around small, independent services that work together to form the whole application
- `Microservices` has each piece (e.g. auth, customer data, product data, ...) acting as completely separate executable
- `Microservices` has parts with many replicas (e.g. search and product data)
- `Microservices` has parts each scaling separately


## Advantages of Microservices

1. Scalability
    - `Microservices` allows each part to be independtly scalable
    - `Microservices` allows resources to be used more efficiently
        - in `Monolithic` application, whole thing needs to be scaled
2. Cleaner Code
    - `Microservices` has more independence between different pieces of application
    - `Microservices` allows easier maintaince of application 
    - `Microservices` enforces cleaner code
3. Reliability
    - `Microservices` is less likely to affect the application overall when there is:
        1. A bug
        2. performance issue
        3. other issues
4. Variety of Tools
    - `Microservices` allows to use a wider variety of tools
    - `Microservices` allows usage of appropriate tool for each individual job
    - `Microservices` allows different parts of application to be
        1. built using different programming languages
        2. built using different framework
        3. built using different architecture


## Disadvantages of Microservices
1. Increased complexity
    - This is where Kubernetes come in

## Note
- The more independent the code is, the less likely it is to negatively affect one another

#