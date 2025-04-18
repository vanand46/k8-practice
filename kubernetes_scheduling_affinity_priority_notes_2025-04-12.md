# 🗓️ Notes: April 12, 2025

> Quick tip:  
> Alias for convenience — `$ alias k8=kubectl`

---

## 🔹 Scheduling in Kubernetes

The **Kubernetes Scheduler** determines the optimal node to run a pod, based on cluster status and resource requirements.

### Key Concepts
- Scheduler works with **controller manager** and **etcd** to evaluate node availability.
- You can **manually assign pods to nodes**, bypassing the scheduler.
- You can target nodes using **labels, selectors, and affinity rules**.

### Direct Pod Scheduling
```bash
k8 explain pod.spec.nodeName  # Assign a pod to a specific node
```
- In this case, the **API server** creates the pod, not the scheduler.
- You can verify this via the `From` field in the pod's event logs.

### Using Node Labels and Selectors
```bash
k8 label node <node-name> disktype=ssd
k8 explain pod.spec.nodeSelector
```
- **nodeSelector** selects nodes based on matching labels.
- If a matching node isn't found, pod stays in `Pending` state.

### Affinity & Anti-Affinity

Affinity rules define conditions that help the scheduler choose a node.

#### Node Affinity (`nodeAffinity`)
- **RequiredDuringSchedulingIgnoredDuringExecution**  
  → Mandatory: Pod won’t schedule if condition isn’t met.
- **PreferredDuringSchedulingIgnoredDuringExecution**  
  → Weighted preference: Tries to match, but not mandatory.

#### Pod Affinity (`podAffinity`)
- Pods prefer to be **co-located** with other pods (e.g., on the same node).
- Useful for services that need to run together.

#### Pod Anti-Affinity (`podAntiAffinity`)
- Pods prefer **NOT** to be placed on the same node.
- Prevents overloading a single node with the same pod types.

---

## 🔹 Taints and Tolerations

Taints prevent pods from being scheduled onto nodes **unless** they have matching tolerations.

- **Taint** acts like a "lock" on a node.
- **Toleration** is the "key" that allows the pod to be scheduled there.

Use this mechanism to:
- Keep certain workloads (like control-plane pods) isolated
- Avoid accidental pod placement on sensitive nodes

---

## 🔹 Pod Priority and Preemption

Used to schedule more critical pods **before** others when resources are limited.

- Define priorities via **PriorityClasses**.
- Add `priorityClassName` to your pod spec.

High-priority pods can **evict lower priority pods** if needed.

---

## 🔹 Security Context

Defines security-related options for pods and containers.

> *To be expanded with usage examples and fields like `runAsUser`, `fsGroup`, etc.*

---

## 🧪 TODO: Lab Practice  
- Schedule pods on specific nodes using `nodeName` and `nodeSelector`.
- Use node/pod affinity and anti-affinity in scheduling rules.
- Configure taints on nodes and create pods with matching tolerations.
- Create `PriorityClass` resources and assign them to pods.
- Experiment with `securityContext` settings inside pod specs.
