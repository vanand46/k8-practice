
# 🗓️ Notes: April 19, 2025

## 🔹 Storage Concepts in Kubernetes

- **Pod-level sharing**: Share data between two pods on the same node.
- **Container-level sharing**: Share data between multiple containers **within the same pod**.

> ⚠️ When a pod is deleted, all data stored **within** the pod (unless backed by persistent volumes) is lost.  
> Data stored directly inside containers is **non-persistent** by default.

---

## 🔹 Volume Configuration

### 📦 `volumeMounts`  
Use `kubectl explain pod.spec.volumes` to explore volume configuration.  
- Volumes define **named storage units** available to all containers in a pod.
- Each container can choose to **mount** any declared volume.

### 📁 Volume Types

- **emptyDir**:  
  - Temporary directory that exists as long as the pod exists.  
  - Ideal for sharing data between containers in the same pod.
  
- **hostPath**:  
  - Mounts a file or directory from the host node’s filesystem into the pod.
  
- **configMap**:  
  - Mount configuration data from external files into the container.
  
- **persistentVolume (PV)**:
  - Enables long-term storage **beyond the pod lifecycle**.
  
  #### PV Types

  - **On-Premise Options**:
    - SAN, NFS, iSCSI, Cinder, CephFS, Portworx (K8s-native)

  - **Cloud-native Options**:
    - AWS: EBS
    - GCP: Persistent Disk
    - Azure: Managed Disks, Files
    - Any block storage services supported by the cloud provider

---

### 📋 Persistent Volume Workflow

1. **Create a Persistent Volume (PV)**  
   - Usually provisioned by a separate team (external resource, not in-app).
2. **Create a Persistent Volume Claim (PVC)**  
   - Defined in your K8s application to "claim" a matching PV.
   - One PV is bound to one PVC.
3. **Mount the PVC**  
   - Use it in the pod just like any other volume.

---

### 🔐 Access Modes

- `ReadWriteOnce` – Mounted as read-write by a single node.
- `ReadOnlyMany` – Mounted as read-only by multiple nodes.
- `ReadWriteMany` – Mounted as read-write by multiple nodes.

---

## 🛠️ Volume Setup Example

### 1️⃣ Define the Volume in Pod Spec
```yaml
volumes:
  - name: xchange
    emptyDir: {}
```

### 2️⃣ Mount It in the Container
```yaml
volumeMounts:
  - name: xchange
    mountPath: "/tmp/data"
```
