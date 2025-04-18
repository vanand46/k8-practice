# 🗓️ Notes: April 06, 2025

> Quick tip:  
> Alias for convenience — `$ alias k8=kubectl`

---

## 🔹 Labels and Selectors

Labels are key-value pairs attached to resources (like pods, nodes) and selectors are used to filter them.

### Commands
```bash
k8 get pods --show-labels
k8 get nodes --show-labels
k8 get nodes -l beta.kubernetes.io/os=linux
k8 get pods -l tier=backend -l role=master
kubectl get pods -l 'tier in (backend), role notin (slave)'
```

---

## 🔹 Self-Healing Pods: Liveness & Readiness Probes

These are **health checks** that Kubernetes uses to manage container lifecycle and ensure stability.

### Liveness Probe
- Checks if the app is still running.
- **Failure → Container is restarted.**
- Common parameters:
  - `initialDelaySeconds`
  - `periodSeconds`

### Readiness Probe
- Checks if the app is ready to **accept traffic**.
- **Failure → Traffic is not sent to the pod.**
- The container stays running, but is temporarily removed from service.

### Status Lifecycle
1. **Running**
2. **Health checks run**
3. Becomes **READY** only if checks pass

---

## 🔹 Auto Scaling with Metrics Server

Kubernetes can **automatically scale** the number of pods based on CPU or custom metrics.

### Why Metrics Server?
- Kubernetes doesn’t include a metrics collection system by default.
- **Metrics Server** is used to collect CPU/memory usage to aid in autoscaling decisions.

### Steps to Set Up
1. Install Metrics Server
2. Start collecting metrics
3. Set autoscaling criteria

### Example
```bash
k8 autoscale deploy frontend --min=3 --max=6 --cpu-percent=40
```

---

## 🔹 Namespaces

Namespaces logically isolate Kubernetes resources.

### Why use Namespaces?
- Group services by team, department, or purpose.
- Manage **resource quotas**.
- Enforce **RBAC (Role Based Access Control)**.

### Commands
```bash
k8 get ns
k8 get pod -n kube-system
k8 create ns facebook
k8 get ns facebook -o yaml
```

- **Default namespace** is used when none is specified – not a best practice.
- You can define a namespace in:
  - YAML metadata (`metadata.namespace`)
  - CLI using `-n` flag:
    ```bash
    k8 apply -f <file>.yaml -n facebook
    ```

---

## 🔹 Helm – Templating & Packaging Tool

Helm simplifies deploying Kubernetes applications via reusable charts.

### Features
- Chart = Package containing pre-configured Kubernetes resources
- Templating = Customizing resource manifests

### Setup & Usage

#### Install Helm
```bash
sudo snap install helm --classic
```

#### Manage Repos
```bash
helm repo ls
helm repo add <repo-name> <repo-url>   # bitnami is a popular choice
helm repo update
```

#### Install & Manage Releases
```bash
helm search repo <chart-name>
helm install dev-nginx bitnami/nginx
helm install stg-nginx bitnami/nginx --values stage-var.yaml
helm upgrade stg-nginx bitnami/nginx --values stage-var.yaml
helm uninstall stg-nginx
```

---

## 🧪 TODO: Lab Practice  
- Practice using labels and selectors with various resources.
- Configure and test liveness & readiness probes.
- Install metrics server and set up auto scaling.
- Create and manage namespaces using both CLI and YAML.
- Explore Helm charts – install, override values, and upgrade them.
