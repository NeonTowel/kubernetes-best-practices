# Kubernetes Production Best Practices Checklist

## Health Checks
- [ ] **Readiness probes** configured to determine when containers can receive traffic  
- [ ] **Liveness probes** configured as passive recovery mechanism (not for fatal errors)  
- [ ] No shared endpoints between liveness and readiness probes  
- [ ] Let containers crash immediately on unrecoverable errors instead of failing probes  
- [ ] Applications handle SIGTERM for graceful shutdowns  
- [ ] Implement preStop hooks for connection draining  
- [ ] Close idle keep-alive connections before termination  

## Fault Tolerance
- [ ] Deploy multiple replicas using Deployments/ReplicaSets  
- [ ] Configure pod anti-affinity rules across nodes  
- [ ] Set Pod Disruption Budgets for minimum availability  
- [ ] Test graceful shutdown with kube-sigterm-test tool  

## Resource Management
- [ ] Set memory limits/requests for all containers  
- [ ] Configure CPU requests ≤ 1 for most workloads  
- [ ] Consider disabling CPU limits unless required  
- [ ] Implement LimitRange in namespaces  
- [ ] Set appropriate Quality of Service (QoS) classes  

## Tagging & Metadata

- [ ] Resources have technical labels defined
- [ ] Resources have business labels defined
- [ ] Resources have security labels defined

**Technical Labels example**
- app.kubernetes.io/name: user-api
- app.kubernetes.io/version: "42"
- app.kubernetes.io/component: api

**Business Labels example**
- owner: payment-team
- project: fraud-detection
- business-unit: "80432"

**Security Labels example**  
- confidentiality: official
- compliance: pci

## Logging
- [ ] Applications log to stdout/stderr (12-factor app principle)  
- [ ] Avoid logging sidecars when possible  
- [ ] Implement centralized logging (EFK stack, CloudWatch, etc.)  
- [ ] Maintain 30-45 day log retention  

## Scaling
- [ ] Use Horizontal Pod Autoscaler (HPA) for variable loads  
- [ ] Avoid Vertical Pod Autoscaler (VPA) in production  
- [ ] Consider Cluster Autoscaler for node-level scaling  
- [ ] Store persistent data externally (no local filesystem state)  

## Configuration & Secrets
- [ ] Externalize configuration via ConfigMaps  
- [ ] Mount Secrets as volumes (not environment variables)  
- [ ] Implement ResourceQuotas in namespaces  

## Security
- [ ] Disable privileged containers  
- [ ] Use read-only root filesystems  
- [ ] Run containers as non-root users  
- [ ] Drop all Linux capabilities by default  
- [ ] Prevent privilege escalation  
- [ ] Enable Network Policies for namespace isolation  

## Cluster Compliance
- [ ] Pass CIS Kubernetes Benchmark using kube-bench  
- [ ] Disable cloud metadata API access  
- [ ] Restrict alpha/beta features  

## RBAC & Authentication
- [ ] Disable default ServiceAccount auto-mounting  
- [ ] Implement least-privilege RBAC policies  
- [ ] Use OpenID Connect (OIDC) for user authentication  
- [ ] ServiceAccount tokens only for apps/controllers  

## Custom Policies
- [ ] Restrict container registries via admission controllers  
- [ ] Enforce unique Ingress hostnames  
- [ ] Validate Ingress domains with OPA  
