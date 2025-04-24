# 🗓️ Notes: April 19, 2025

## Storage
- Share data between two pods in the same node.
- Share date between two containers within the pod
 
 When we delete a pod, the data within the pod is will get deleted.
 The data stored in the container is non persisted.
 
## Volume Config
- volumeMounts (`kubectl explain pod.spec.volumes`)
List of volumes that can be mounted by containers belonging to the pod.
Volume represents a named volume in a pod that may be accessed by any container in the pod.

### Volume Types
- emptyDir : represents a temporary directory that shares a pod's lifetime.Used for sharing the data bewtween containers within the pods.
- hostPath : hostPath represents a pre-existing file or directory on the host machine that is directly exposed to the container.

## Steps in Volume Creation
- Create the volume for the pod
```yaml
volumes:
- name: xchange
  emptyDir: {}
```
- Attach the volume to the container 
```yaml
volumeMounts:
  - name: xchange
    mountPath: "/tmp/data"
```
