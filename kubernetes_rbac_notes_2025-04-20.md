
# 🗓️ Notes: April 20, 2025

## 🔹 Roles and Role Binding

- **Role** = **Resources** + **Permissions** (verbs).
- **Authentication** = Verifying identity (login).
- **Authorization** = Granting access (roles and permissions).

---

## 🔹 Kubernetes RBAC (Role-Based Access Control)

### 📋 Permissions (Verbs) for K8s Resources

- `create`
- `read` (includes `list`, `get`, `watch`)
- `update`
- `patch`
- `delete`

---

### 📄 Roles

- Defined by:
  - **Resources** + **Verbs** + **Namespace**

### 🔗 RoleBinding

- Connects:
  - **Role** + **User/Group/Service Account (SA)** + **Namespace**

---

## 🔹 Application Onboarding in Kubernetes Cluster

Steps:
1. Create a **namespace**.
2. Set **resource quotas** for the namespace.
3. Create **Role** and **RoleBinding** for namespace access.
4. Deploy application resources **inside the namespace**.

---

## 🔹 Super Admin Responsibilities

- Handle critical tasks like **application onboarding** into the cluster.
- Manage namespace setup, quotas, and initial access.

---

## 🔹 Cluster Administrators

- **ClusterRole**:  
  - Similar to Role but **not namespace-scoped**.
  - Applies **cluster-wide**.

- **ClusterRoleBinding**:  
  - Connects a **ClusterRole** with **User/Group/ServiceAccount**.

- Useful command:
  ```bash
  kubectl get clusterrole
  ```

---

## 🔹 Resource Quota Management

- **Resource Quota**:  
  - Controls total resource consumption within a namespace.

- ⚠️ Important:
  - Reserve **25%** of cluster resources for `kube-system` components.
  - Keep **30%** of resources **free** for cluster operations.

---
