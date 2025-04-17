# 🗓️ Notes: April 05, 2025

## 🔹 Deployment in Kubernetes

### Deployment Basics
- Use `kubectl api-resources | grep deployment` to verify if Deployment is a supported resource.
- A Deployment manages **replica sets** and **pod templates** to ensure the desired state of an application is maintained.
- Key YAML fields:
  - `kind: Deployment`
  - `template:` – Specifies pod template (metadata + spec).
  - `replicas:` – Number of pod instances to maintain.

### Basic Commands
- Apply a deployment:
  ```bash
  kubectl apply -f deploy.yaml
  ```
- Get current deployments:
  ```bash
  kubectl get deploy
  ```

### Deployment Output Columns
- `READY` – Shows how many pods are running (`n/n` format).
- `UP-TO-DATE` – Shows pods updated with the latest revision.

### Update Strategies

#### 🔁 Rolling Update (Canary Style)
- Safely updates pods **one at a time**.
- No downtime.
- **Not recommended** for breaking changes or completely new features.
- New pod created → Verified → Old pod removed.

#### 🟦🟩 Recreate (Blue/Green Style)
- Creates a **new set of pods** while keeping the old ones.
- Deletes old pods **after** new ones are running.
- May cause **downtime**.
- Best suited for **breaking changes or brand new features**.

### Deployment Management

- **Update image via YAML** – Edit the deployment YAML and reapply.
- **Update image via command:**
  ```bash
  kubectl set image deployment nginx-deployment nginx=nginx:<version>
  ```
- **View rollout history:**
  ```bash
  kubectl rollout history deploy nginx-deployment --revision=<number>
  ```
- **Rollback to previous revision:**
  ```bash
  kubectl rollout undo deploy nginx-deployment
  ```
- **Rollback to specific revision:**
  ```bash
  kubectl rollout undo deploy nginx-deployment --to-revision=1
  ```

### Manual Scaling
- Scale up:
  ```bash
  kubectl scale deploy nginx-deployment --replicas=5
  ```
- Scale down:
  ```bash
  kubectl scale deploy nginx-deployment --replicas=2
  ```
- Stop deployment (cost-saving):
  ```bash
  kubectl scale deploy nginx-deployment --replicas=0
  ```

---

## 🔹 DaemonSet

- **DaemonSet** ensures a pod runs **on all (or specific) nodes**.
- Common use cases: **log collection**, **monitoring agents**.
- `kind: DaemonSet`
- No need to define replicas – it matches the number of nodes.

### DaemonSet Commands
- View daemonsets:
  ```bash
  kubectl get ds
  ```
- View system daemonsets:
  ```bash
  kubectl get ds -n kube-system
  ```

> 💡 FYI: “k8s” stands for Kubernetes – with “8” letters between “k” and “s”.

---

## 🔹 Configuration in Kubernetes

### Environment Variables
- Basic setup using env vars inside pod/container definitions.
- Good for **small and simple configs**.

### ConfigMap
- Used to store **non-sensitive key-value pairs**.
- Externalize configuration from container images.

### Secret
- Used to store **sensitive information** like passwords, tokens, and SSH keys.
- Base64-encoded values.

---

## 🧪 TODO: Lab Practice  
- Hands-on practice required for:
  - Creating and updating deployments with different strategies.
  - Scaling up/down manually.
  - Using DaemonSets.
  - Managing config via ConfigMaps and Secrets.
- Refer to **Google Doc titled "Workload"**
