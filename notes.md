# April 13, 2025
## Networking
### Network Types
- Management/Cluster Network (Control Plane & Worker Node) - 172.31(here only)
- Pod Network - 192.168.0.0/16 (here only)
- Service Network - 10.96.0.0/12 (here only)
### Container Network Interface
- Calico - which famous plugin for managing network
- Flannel and Weavenet is some other networking plugins
- Manages the network of container or pods

## Cloud Workflow
User -> Load Balancer -> Auto Scaling (EC2-1, EC2-2) 
## Kubernetes
User -> Load Balancer(Service (svc)) -> Deployment (Pod1, Pod3)

## Service (SVC)
- It acts as a Load Balancer of the cluster.
- Configuration of Service is defined in manifest of API server
- `$ k8 get svc` // To see the list of services
- `$ k8 explain svc`
- `$ k8 explain svc.spec`

The direct communication between pods are not recommended.It has usually done with services.

- Pod labels and selectors are used by services to identify the pods.
- Service Port
- Target Port
- Container Port
- Service Port -> Target Port -> Container Port
- Target Port === Container Port
- kube-proxy managing services which is a configuration.
- `$ k8 get ep <service-name>` // The Entrance Point

### Service Types
Based on the traffic, we decide the service type.
- LoadBalancer
    - Internet Traffic
    - amazon, facebook are some of the examples.
- NodePort
    - External Load Balancer
    - External Traffic within Organisation
    - Intranet, JIRA(Agile Framework), Jenkins, Git are the some of the examples
    - Port Range [30000 - 32767] - 2767
- ClusterIP 
    - Default service Type
    - Internal Load Balancer
    - Internal Traffic
    - Redis, DB, Kafka are the some of the examples

## DNS
- Resource Name to IP mapping.
- `$ k8 get deploy -n kube-system` // we can see core dns in the output list of the command
- `$ k8 get svc -n kube-system`
There will be kube-dns service of the type ClusterIP in the system

### Types of communications
- Pod to service in same name space
- Pod to service in different name space (not a good practice)
- Pod to Pod communication
- Pod to Pod communication in different name space

## 

