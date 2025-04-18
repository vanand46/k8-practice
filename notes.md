# April 6, 2025

Quick note: `$ alias k8=kubectl`

## Labels and Selectors
- `$ k8 get pods --show-labels`
- `$ k8 get nodes --show-labels`
- `$ k8 get nodes -l beta.kubernetes.io/os=linux`
- `$ k8 get pods -l tier=backend -l role=master`
- `$ kubectl get pods -l 'tier in (backend), tole notin (slave)'`

## Self Healing Pods - Liveness Probe and Readiness Probe (Health Check)
Two different status
- Running
- Basic Checks
- Then READY state
- This handles how it become to reday state when spinning up more pods
- `livenessProbe`
    - `initialDelaySeconds`
    - `periodSeconds`
    - When livenessProbe fails, the container will restart.
- `readinessProbe`
    - When readinessProbe fails, the service will not send traffic to the container and other will fix the issue by restarting the container. 

## Auto scaling
Automatically increase/decrease the number of pods based on various parameters of the resources.

### Metrics Server

Which is used to collect the metrics of the clustter to decide the scalling scenarios.We use this since the k8 does not have any metrics collection and monitoring platforms in built.

### Steps
- Install metrics server
- Collect metrics
- Set the autoscalling scenarios based on the metrics

`$k8 autoscale deploy frontend --min 3 --max --6 --cpu-percent 40`

## Namespaces
Grouping the services and application based on some criteria for example by product, department or service ...etc.

- We can set the resource quotas  by considering the namespaces concept.
- Can be used for Role Based Access Control
- `$ k8 get ns`
- `$ k8 get pod -n kube-system`
- There is a default name space is avaible in which all resoureces are created if we not provide the namespace.(not a good practice)
- `$ k8 create ns facebook`
- `$ k8 get ns facebook -o yaml`
- We can also create namespace using YAML file using the kind as `Namespace`
- Create the resources under a namespace
    - By mentioning the namespace within the metadata section of the YAML configuration file of the resource.(hard-coded method)
    - During the deployment 
        - `$ k apply -f <file-name>.yaml -n facebook`

## Helm - Package Manager



