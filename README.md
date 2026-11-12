# Kubernetes Production Operations

**Project Owner:** Richard Jabarul Akbar

## Overview

A hands-on Kubernetes production operations
and cluster administration project.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes
- KodeKloud Playground
- containerd
- Calico
- Helm
- NGINX
- Prometheus

## Project Status

Implementation in progress.

## Repository Structure

- application/
- architecture/
- manifests/
- networking/
- operations/
- backup-recovery/
- monitoring/
- scripts/
- evidence/

## Author

Richard Jabarul Akbar
## Project Checkpoints

### CP-07: Kubernetes Services & Ingress

Implemented and validated Kubernetes service networking
and HTTP ingress routing.

**Services:**
- ClusterIP with CoreDNS service discovery
- NodePort tested across all three cluster nodes
- LoadBalancer service created (external IP pending)

**Ingress:**
- F5 NGINX Ingress Controller v5.7.1
- NodePort HTTP: 30080
- NodePort HTTPS: 30443
- Host-based routing using `nginx.local`
- Unknown hostname correctly returns HTTP 404

**Documentation:**
- [Services & Ingress](services/services-ingress.md)
- [Service Manifests](services/nginx-services.yaml)
- [Ingress Manifest](services/nginx-ingress.yaml)
