# 🗓️ Notes: March 30, 2025

## 🔹 POD Basics
- Pods are **immutable** units in Kubernetes.
- Each pod can contain **multiple containers**, including **supporting/init containers**.
- **IP addresses** are assigned to pods.
- Access to pods is done using **ports**.

## 🔹 Useful `kubectl` Commands
- `kubectl api-resources` – List all available resources.
- `kubectl explain <resource-name>` – Describe a resource.
- `kubectl explain <resource-name> --recursive` – Deeply describe a resource.
- `kubectl get ns` – View all namespaces:
  - `default`
  - `kube-node-lease`
  - `kube-public`
  - `kube-system`
- `kubectl get pods -n kube-system` – View system pods.
- `kubectl apply -f <file-name>.yaml` – Apply a YAML manifest.
- `kubectl get pod <pod-name> -o yaml` – Get pod description in YAML.
- `kubectl get pod <pod-name> -o json` – Get pod description in JSON.

## 🔹 Key Manifest Fields
- `apiVersion` – Version of the Kubernetes API.
- `kind` – Type of the resource (e.g., Pod, Service).
- `metadata` – Metadata info (name, labels, etc.).
- `spec` – Infrastructure configuration.

## 🔹 Init Containers
- Run **before** main containers.
- Used for setup tasks like:
  - Retrieving secrets (e.g., DB username/password)
  - Connection checks
- Defined under the `initContainers` section in the pod spec.
- Main containers start **only after** all init containers succeed.

## 🔹 Cluster Management
- `kubeadm` – Tool to create/control the Kubernetes control plane.
- `kubelet` – Runs on the master node and manages **static pods** (includes control plane pods).

## 🔹 Resource Management
- Set **CPU and memory** limits for containers.
- Not setting limits may lead to **performance issues** on the host machine.

---

## 🧪 TODO: Lab Practice  
- Refer to **Google Doc titled "Workload"**

---

## 📊 Kubernetes Dashboard
- Setup guide: [Kubernetes Web UI Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)
- Command: `kubectl get all -n kubernetes-dashboard`
