# April 05, 2025

## Deployment
- `kubectl api-resources | grep deployment`
- PodTemplate
- Kind: Deployment
- Template
- Replicas
- `kubectl apply -f deploy.yaml`
- `kubectl get deploy`
    - READY - Total number of pods n/n n out of n are running
    - Update Pods
        - Rolling Update Canary
            - Create a new pod with new image
            - Then old pod will get deleted , add new pods one at a time(no down time)
            - Incremental update is suitable.For the new feature it is not recommneded
        - Recreate - BlueGreen
            - Two nodes are created 
            - Two nodes are  deleted.
            - Downtime and recommended for new features and breaking changes with images.
        - Upadate image through YAML
        - `kubectl rollout history deploy nginx-deployment --revision=<number>`
        - `kubectl set image deployment nginx-deployment nginx=nginx:<version>`
        - UP-TO-DATE - the new revison pods status
        - To rollback - `kubectl rollout undo deploy nginx-deployment`
        - To rollback to specific revision - `kubectl rollout undo deploy nginx-deployment --to-revision=1`
        - SCALE Manual Method `kubectl scale deploy nginx-deployment --replicas 5`
        - SCALE Manual Method `kubectl scale deploy nginx-deployment --replicas 2`
        - SCALE Manual Method `kubectl scale deploy nginx-deployment --replicas 0` // 0 cost
        - Daemon Sets - Used to launch common containers for all nodes example log aggregation
            - `DaemonSet` a kind
            - it is same as deployment but there is no concept of replicas since it will be equal to the number of nodes
            - `kubectl get ds`
            - `kubectl get ds -n kube-system`
            - k8s means k 8 letter between k and s
### Configuration
            





