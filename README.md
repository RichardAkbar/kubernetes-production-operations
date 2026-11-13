
# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

# Kubernetes Production Operations

**Project Owner:** Richard Jabar Akbar

## Overview

A hands-on Kubernetes production operations project focused on cluster administration, networking, workload management, persistent storage, troubleshooting, backup and recovery, and monitoring.

This project demonstrates practical Kubernetes administration and operational procedures in a multi-node KodeKloud Kubernetes environment.

## Objectives

- Kubernetes Multi-Node Administration
- Cluster Networking and CNI
- Workload Management
- Services and Ingress
- Persistent Storage
- Production Troubleshooting
- ETCD Backup and Recovery
- Monitoring and Observability

## Technology Stack

- Kubernetes v1.37.0
- containerd
- Calico
- Helm
- NGINX Ingress Controller
- Prometheus
- Grafana
- Alertmanager
- ETCD

## Project Status

**Implementation completed — CP-01 through CP-10.**

All planned project checkpoints have been implemented and documented. Validation was performed in the KodeKloud Playground environment.

## Project Checkpoints

### CP-01 — Repository Setup
Repository structure and project foundation.

### CP-02 — Environment Assessment
Kubernetes environment and cluster assessment.

### CP-03 — Kubernetes Architecture
Multi-node cluster architecture and documentation.

### CP-04 — Cluster Administration
Cluster administration and operational validation.

### CP-05 — Networking & CNI
Kubernetes networking and Calico validation.

### CP-06 — Workload Management
Deployment, scaling, and workload operations.

### CP-07 — Services & Ingress
- ClusterIP and NodePort services
- LoadBalancer service configuration (external IP pending in lab)
- F5 NGINX Ingress Controller v5.7.1
- Host-based routing using `nginx.local`
- HTTP routing validation

Documentation: [Services & Ingress](services/services-ingress.md)

### CP-08 — Persistent Storage
- PersistentVolume and PersistentVolumeClaim
- hostPath storage configuration
- Pod storage mounting
- Data persistence validation after Pod recreation

Documentation: [Storage Management](storage/storage-management.md)

### CP-09 — Production Operations
- Cluster health assessment
- ImagePullBackOff troubleshooting
- CrashLoopBackOff troubleshooting
- Resource requests and limits inspection
- Deployment self-healing validation

Documentation: [Production Operations](operations/production-operations.md)

### CP-10 — Backup, Monitoring & Finalization

**ETCD Backup and Recovery**
- ETCD snapshot creation
- Snapshot integrity verification using SHA256
- Offline restore validation using etcdutl
- Kubernetes cluster health verification after isolated restore

Documentation: [ETCD Backup & Recovery](backup-recovery/etcd-backup-recovery.md)

**Monitoring and Observability**
- Prometheus and Grafana deployment using Helm
- Alertmanager and kube-state-metrics
- Kubernetes resource dashboard validation
- Prometheus target health validation
- PromQL query execution

Monitoring validation observed 19 targets UP and 9 targets DOWN out of 28 targets at the time of testing.

Node Exporter was disabled due to host filesystem mount restrictions in the lab environment. Prometheus and Grafana used non-persistent storage configuration because no StorageClass was available.

Documentation: [Monitoring & Observability](monitoring/monitoring-observability.md)

## Repository Structure

```text
.
├── architecture/
├── backup-recovery/
├── manifests/
├── monitoring/
├── networking/
├── operations/
├── services/
├── storage/
├── workloads/
├── monitoring-values.yaml
├── .gitignore
└── README.md
```

## Environment Limitations

This project was implemented in an ephemeral KodeKloud Playground environment.

- Lab resources may be reset.
- Local hostPath storage is not highly available.
- ETCD offline restore was tested in an isolated data directory, not as a complete cluster disaster recovery.
- Monitoring persistence was disabled.
- Some Prometheus scrape targets were unavailable during validation.
- Node Exporter was disabled due to mount propagation restrictions.

These limitations are documented to distinguish lab validation from a production deployment.

## Security

- ETCD snapshots and Kubernetes secrets are excluded from the public repository.
- Credentials and private keys must not be committed.
- Monitoring access should be protected.
- Backup files should be stored in secure external storage.

## Author

**Richard Jabar Akbar**

