# Kubernetes Antipatterns to Avoid

## Table of Contents
- [Cluster Management](#cluster-management)
- [Security Pitfalls](#security-pitfalls)
- [Networking Mistakes](#networking-mistakes)
- [Resource Mismanagement](#resource-mismanagement)
- [Deployment Issues](#deployment-issues)
- [Storage Misconfigurations](#storage-misconfigurations)
- [Monitoring and Logging Failures](#monitoring-and-logging-failures)
- [CI/CD Mistakes](#ci-cd-mistakes)
- [Vulnerability and Risk Management Issues](#vulnerability-and-risk-management-issues)

---

## Cluster Management
❌ **Running a Single-Master Cluster in Production**  
➡️ Always use at least three control plane nodes for high availability.

❌ **Manually Managing Node Scaling**  
➡️ Use Cluster Autoscaler to automatically adjust the number of nodes.

❌ **Using the Default Namespace for All Deployments**  
➡️ Define separate namespaces for logical isolation of workloads.

---

## Security Pitfalls
❌ **Running Containers as Root**  
➡️ Use a non-root user in container images and enforce securityContext.

❌ **Hardcoding Secrets in Environment Variables**  
➡️ Store secrets in Kubernetes Secrets and mount them securely.

❌ **Exposing Kubernetes API to the Internet**  
➡️ Restrict API access using firewall rules and RBAC policies.

❌ **Overly Permissive RBAC Roles**  
➡️ Follow the principle of least privilege and restrict user access.

---

## Networking Mistakes
❌ **Allowing All Traffic Between Pods**  
➡️ Use NetworkPolicies to restrict unnecessary communication.

❌ **Using IP-Based Whitelisting Instead of Service Identities**  
➡️ Implement service mesh authentication (e.g., Istio mTLS).

❌ **Hardcoding IP Addresses in Configurations**  
➡️ Use Kubernetes Service DNS names instead of static IPs.

---

## Resource Mismanagement
❌ **Not Setting Resource Requests and Limits**  
➡️ Define CPU and memory requests/limits to prevent resource starvation.

❌ **Over-Provisioning Nodes Without Autoscaling**  
➡️ Enable Horizontal Pod Autoscaler (HPA) and Cluster Autoscaler.

❌ **Ignoring Pod Evictions and OOMKills**  
➡️ Monitor and adjust resource quotas to prevent frequent pod restarts.

---

## Deployment Issues
❌ **Using `latest` Tag for Container Images**  
➡️ Always use versioned tags to ensure reproducible deployments.

❌ **Not Using Readiness and Liveness Probes**  
➡️ Define health checks to restart failing applications automatically.

❌ **Deploying Stateful Applications Without PersistentVolumes**  
➡️ Use PersistentVolumeClaims (PVCs) to store critical application data.

---

## Storage Misconfigurations
❌ **Using HostPath for Persistent Storage**  
➡️ Use dynamically provisioned PersistentVolumes instead of HostPath.

❌ **Not Backing Up Persistent Data**  
➡️ Implement scheduled backups using Velero or a cloud-native solution.

❌ **Misconfiguring StorageClass and Retention Policies**  
➡️ Choose appropriate storage classes and define proper reclaim policies.

---

## Monitoring and Logging Failures
❌ **Not Collecting Cluster Metrics and Logs**  
➡️ Deploy Prometheus, Grafana, and Loki/Fluentd for observability.

❌ **Ignoring Pod CrashLoopBackOff Events**  
➡️ Investigate failing pods and use Kubernetes Events to diagnose issues.

❌ **Not Setting Up Alerts for Critical Failures**  
➡️ Configure alerting systems for CPU spikes, memory leaks, and API failures.

---

## CI/CD Mistakes
❌ **Not Using Declarative Infrastructure as Code (IaC)**  
➡️ Use tools like Helm, Kustomize, or GitOps (ArgoCD, Flux) to manage Kubernetes configurations.

❌ **Skipping Deployment Rollback Strategies**  
➡️ Use Kubernetes rollbacks or progressive deployment strategies like canary and blue-green deployments.

❌ **Building and Pushing Images Directly from CI/CD Pipelines**  
➡️ Use a separate build system (e.g., Docker BuildKit, Kaniko) to generate images and push them to a registry.

---

## Vulnerability and Risk Management Issues
❌ **Not Regularly Scanning Images for Vulnerabilities**  
➡️ Integrate vulnerability scanning tools like Trivy or Clair into the CI/CD pipeline.

❌ **Ignoring Dependency Updates in Container Images**  
➡️ Regularly update base images and dependencies to patch security vulnerabilities.

❌ **Allowing Unrestricted Image Pulls from Public Registries**  
➡️ Use private image registries and enforce policies to allow only signed and trusted images.

❌ **No Security Policies for Workloads**  
➡️ Implement policies with Kyverno or OPA Gatekeeper to enforce security best practices.
