# April 13, 2025

> Quick tip: `$ alias k8=kubectl`

## Networking in Kubernetes

### Network Types
- **Management / Cluster Network** (Control Plane & Worker Node): Typically uses `172.31.x.x` range.
- **Pod Network**: Network between pods, typically `192.168.0.0/16`.
- **Service Network**: Used by Kubernetes services, default is `10.96.0.0/12`.

### Container Network Interface (CNI)
- **Calico**: Popular CNI plugin for networking and network policies.
- **Flannel**, **WeaveNet**: Other common plugins for managing pod networking.
- CNIs manage IP allocation and routing for pods across nodes.

## Cloud Workflow
**User → Load Balancer → Auto Scaling Group (EC2-1, EC2-2)**

## Kubernetes Traffic Flow
**User → Load Balancer (Service) → Deployment → Pod(s)**

## Kubernetes Services (svc)
- Acts as an **internal Load Balancer** to expose pods.
- Uses **labels and selectors** to identify and route to appropriate pods.
- `Service Port` → `Target Port` → `Container Port` (targetPort usually equals containerPort).
- Managed by `kube-proxy`.
- `$ k8 get svc` — View available services.
- `$ k8 explain svc.spec` — Explore service configuration.
- `$ k8 get ep <service-name>` — Shows the service’s **endpoints** (linked pods).

### Types of Services
- **ClusterIP** (default):
  - For internal communication only.
  - Examples: Redis, PostgreSQL, Kafka.

- **NodePort**:
  - Exposes the service on a static port on each node.
  - Port range: `30000-32767`.
  - Common for internal tools: Jenkins, GitLab, JIRA.

- **LoadBalancer**:
  - Provisioned by cloud provider.
  - For public-facing services like web servers.

> 📌 Pod-to-pod direct communication is not recommended — use Services.

## DNS in Kubernetes
- Handles resource name → IP resolution.
- CoreDNS manages the internal DNS server.
- `$ k8 get deploy -n kube-system` → Look for `coredns` deployment.
- `$ k8 get svc -n kube-system` → Look for `kube-dns` service.

### Communication Patterns
- Pod → Service (same namespace)
- Pod → Service (cross-namespace) ❗ not recommended
- Pod → Pod (same/different namespace)

## Ingress Controllers
- Ingress accepts external traffic and routes it to internal services.
- Configured via Ingress Resources.
- Automatically updates load-balancing rules when services change.

### Popular Ingress Controllers
- **Nginx** (most common)
- **Traefik**
- **Istio** (advanced service mesh)

### Setup Steps
1. Install an Ingress Controller (e.g., Nginx).
2. Create deployments and services for your app.
3. Define ingress routing using `Ingress` resources.

### Annotations
- Similar to labels but used by **external tools** for extra configuration.
  - e.g., TLS config, rewrite rules, rate limits.

---

## ✅ TODO - Lab Practice
- [ ] Create services with all three types: `ClusterIP`, `NodePort`, `LoadBalancer`.
- [ ] Set up a deployment and expose it via Ingress.
- [ ] Query DNS using service names across namespaces.
- [ ] Use `kube-proxy` logs and `endpoints` to trace routing issues.

