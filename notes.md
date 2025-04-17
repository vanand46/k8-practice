# March 30, 2025
## POD
- POD is immutable
- contains Containers and supporting containers
- IP address assigned to pods
- pods are accessed using ports
- `kubectl api-resources` // listing all resources
- `kubectl explain <resource-name>`
- `kubectl explain <resource-name> --recursive` 
- `apiVersion` - version of the api
- `kind` - kind of the resource
- `metadata` - information of the outside the spec
- `spec`: infra details
- `kubectl get ns`
    - default
    - kube-node-lease
    - kube-public
    - kube-system
- `kubectl get pods -n kube-system`
- `kubectl apply -f <file-name>.yaml` to apply the manifest to API server
- Multiple containers inside the POD
- Init Containers
    [Example] db pod
    - Checks before starting container
    - Getting user name and passwords (from secure storage)
    - Get connection checks
    - After the success of all the init containers , the main containers will start execute
    - `initContainers` section under spec for defining the initContainers
- `kubectl get pod purple -o yaml` ## description pod in the format of  YAML   
- `kubectl get pod purple -o json` ## description pod in the format of  json   
- `kubeadm` is creating the control plane pods and containers
- `kublet` is also running on Master node and which is managing the control plane pods (static pods)
- Add cpu and memory for containers
- If don't set to limit to the resources, then it should affect the performance of the machine is running on containers.

## TO:DO Lab Practice - Google Doc is 'Workload'


## Kubernetes Dashboard

- ref link : https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
- kubectl get all -n kubernetes-dashboard


 
