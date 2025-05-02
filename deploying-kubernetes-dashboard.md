## Deploying the dashboard
- From the master node, execute the following command
  `$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml`
## Verifying the dashboard resources
  ```sh
  $ kubectl get pods -n kubernetes-dashboard -o wide
  $ kubectl get deployment -n kubernetes-dashboard -o wide
  $ kubectl get svc -n kubernetes-dashboard -o wid
  ```
## Editing the Service type of the dashboard
`$ kubectl edit svc -n kubernetes-dashboard kubernetes-dashboard`
  - Change the attribute `type: ClusterIP` to `type: NodePort` (Please note it will open with VI editor)
## Verifying the Service type changes
`$ kubectl get svc -n kubernetes-dashboard -o wide`
 Note down the service(node-port) port number , here it is 30210 
## Checking where the Pod is running
```sh
  $ kubectl get pods -n kubernetes-dashboard -o wide
  $ kubectl get svc -n kubernetes-dashboard -o wide
  $ kubectl get nodes -o wide
```  
## Accessing Kubernetes Dashboard
Click on the master tab on the lab, and then click on the desktop option.
Open Firefox browser 
Or Lauch the Browser on any machine within the intranet and access to the Master Node IP
Then use the following address in Firefox
  https://<localhost/ip of the machine>:30210
  Click on Advanced -> Accept Risk and Continue

On the Kubernetes Dashboard,
Select Token from the given options and enter the token

In Master node
- `$ vi ServiceAccount.yaml`
- Copy and paste the following content inside the file and save it
```YAML
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
```
- `$ kubectl apply -f ServiceAccount.yaml`
- `$ vi ClusterRoleBinding.yaml`
- Copy and paste the following content inside the file and save it
```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: admin-user
    namespace: kubernetes-dashboard
```
- `$ kubectl apply -f ClusterRoleBinding.yaml`
- Now we need to find the token we can use to log in. Execute the following command
- `$ kubectl -n kubernetes-dashboard create token admin-user`
- Copy the token and paste it in Kubernetes Dashboard in Browser.
## [OPTIONAL] Cleanup:
kubectl delete -f  https://raw.githubusercontent.com/kubernetes/dashboard/v2.5.0/aio/deploy/recommended.yaml
## Reference:
https://v1-28.docs.kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md





  
  
  
