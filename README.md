# Kubernetes Core Concepts and Cluster Setup

## Kubernetes Architecture

Kubernetes automates the deployment, scaling, and management of containerized applications. It achieves this through a master-worker architecture.

### Control-Plane Components

The control-plane is the brain of the Kubernetes cluster. It makes global decisions about the cluster (e.g., scheduling) and detects and responds to cluster events.

*   **API Server**: The frontend for the Kubernetes control plane. It exposes the Kubernetes API, which is used by external users and other cluster components to communicate.

*   **etcd**: A consistent and highly-available key-value store used as Kubernetes' backing store for all cluster data.

*   **Scheduler**: Watches for newly created Pods with no assigned node and selects a node for them to run on.

*   **Controller Manager**: Runs controller processes. These controllers include the Node Controller, Replication Controller, Endpoints Controller, and Service Account & Token Controllers.

*   **Cloud Controller Manager (CCM)**: Embeds cloud-specific control logic. It allows you to link your cluster into your cloud provider's API.

### Worker Node Components

Worker nodes are the machines (VMs, physical servers, etc.) where your applications run.

*   **Kubelet**: An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.

*   **Kube-proxy**: A network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

*   **Container Runtime**: The software that is responsible for running containers. Kubernetes supports several container runtimes like Docker, containerd, and CRI-O.

*   **Pods**: The smallest and simplest unit in the Kubernetes object model that you create or deploy. A Pod represents a set of running containers on your cluster.

## Cluster Setup (v1.30)

This section details the commands for setting up a Kubernetes cluster using `kubeadm`.

### Set Hostnames

First, assign unique hostnames to each node in the cluster.

**Master Node:**

```bash
sudo hostnamectl set-hostname master.example.com
exec bash
```

**Worker1 Node:**

```bash
sudo hostnamectl set-hostname worker-node-1.example.com
exec bash
```

**Worker2 Node:**

```bash
sudo hostnamectl set-hostname worker-node-2.example.com
exec bash
```

### Master Node Initialization

Next, initialize the control-plane on the master node.

1.  **Initialize the cluster:**

    ```bash
    sudo kubeadm init
    ```

2.  **Configure kubectl:**
    After `kubeadm init` finishes, it will output a `kubeadm join` command. **Copy this command** to join your worker nodes later. Then, run the following to configure `kubectl`:

    ```bash
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

3.  **Install a Container Network Interface (CNI):**
    A CNI is required for pods to communicate with each other. This example uses Calico.

    ```bash
    kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml
    ```

4.  **Verification:**
    Check the status of the master node.

    ```bash
    kubectl get nodes
    ```

    **Output:**

    ```
    NAME                 STATUS   ROLES                    AGE   VERSION
    master.example.com   Ready    control-plane,master     64m   v1.30.4
    ```

### Worker Node Initialization

Use the `kubeadm join` command you copied earlier to have the worker nodes join the cluster.

1.  **Join the cluster:**
    Run this command on each worker node. **DO NOT COPY AND PASTE THE EXAMPLE BELOW**; use the unique command generated during your `kubeadm init`.

    ```bash
    sudo kubeadm join <cluster-ip>:6443 --token <token> \
        --discovery-token-ca-cert-hash sha256:<hash>
    ```

    If you lose your token, you can generate a new one on the master node:

    ```bash
    sudo kubeadm token create --print-join-command
    ```

2.  **Verification:**
    From the master node, check the status of all nodes.

    ```bash
    kubectl get nodes
    ```

    **Output:**

    ```
    NAME                        STATUS   ROLES                    AGE   VERSION
    master                      Ready    control-plane,master     75m   v1.30.4
    worker-node-1.example.com   Ready    <none>                   72s   v1.30.4
    worker-node-2.example.com   Ready    <none>                   52s   v1.30.4
    ```

## Basic Kubernetes Commands

Here are some fundamental commands for interacting with your cluster.

*   **List all nodes in the cluster:**

    ```bash
    kubectl get nodes
    ```

*   **List all nodes with more detailed information:**

    ```bash
    kubectl get nodes -o wide
    ```

*   **Get detailed information about a specific node:**

    ```bash
    kubectl describe node worker-node-1.example.com
    ```

*   **Create a new pod:**

    ```bash
    kubectl run nginxpod --image nginx
    ```

*   **List all pods:**

    ```bash
    kubectl get pods
    ```

    **Output:**

    ```
    NAME       READY   STATUS    RESTARTS   AGE
    nginxpod   1/1     Running   0          11s
    ```

### Deploying and Accessing a Pod

This example deploys an NGINX pod and shows how to interact with it.

*   **Run an NGINX pod and expose a port:**

    ```bash
    kubectl run nginxpod --image=nginx --port 80
    ```

*   **Get the list of pods:**

    ```bash
    kubectl get pods
    ```

*   **Get detailed information about the pod:**

    ```bash
    kubectl describe pod nginxpod
    ```

*   **Execute a command inside the running container:**

    ```bash
    kubectl exec -it nginxpod -- /bin/sh
    ```

*   **View the logs from the pod:**

    ```bash
    kubectl logs nginxpod
    ```