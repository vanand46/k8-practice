# April 12, 2025

> Quick tip:  
> Alias for convenience — `$ alias k8=kubectl`

## Scheduling
- Scheduler is responsible for creating the pods.
- Scheduler is using control manager and etcd to understand availability and current status of clustter.
- We can use scheduler to create the containers on specific node based on node's hardware features.
- We can bye pass the scheduler and create the containers directly inside nodes.(Need to investigate why Scheduler is not using the node for creating the containers)
- `$ k8 explain pod.spec.nodeName` // where we specify the nodeName here
- In this case api server will create the pod instead of scheduler.We can check it by using the `From` attribute of the Events.
- `$ k8 label node <node-name> disktype=ssd` 
- `$ k8 explain pod.spec.nodeSelector` to select node based on the nodeSelector configuration.
- Challenge is to manage the node is there or not, need to manage duplicate resource names etc..
- If there is issue, then STATUS of the pod is in Pending.

