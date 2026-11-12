# Kubernetes Services & Ingress

## 1. Overview

This phase implements and validates Kubernetes Service types and
NGINX Ingress routing in a multi-node Kubernetes cluster.

The implementation covers:

- ClusterIP Service
- NodePort Service
- LoadBalancer Service
- NGINX Ingress Controller
- Host-based HTTP routing
- Service discovery through CoreDNS

## 2. Environment

| Component | Configuration |
|---|---|
| Kubernetes | v1.37.0 |
| Nodes | 1 Control Plane, 2 Workers |
| Container Runtime | containerd 2.2.3 |
| CNI | Canal (Flannel + Calico) |
| Application | NGINX 1.27 |
| Ingress Controller | F5 NGINX Ingress Controller v5.7.1 |
| Ingress Class | nginx |

## 3. Application Deployment

An NGINX application was deployed in namespace `services-lab`
with two replicas.

Both Pods were scheduled on separate worker nodes.

```bash
kubectl get pods -n services-lab -o wide
