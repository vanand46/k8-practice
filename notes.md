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

- Pod labels and selectors are used by services to identify the pods
