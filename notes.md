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


