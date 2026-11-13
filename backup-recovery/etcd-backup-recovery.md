# ETCD Backup and Recovery

## Overview

This document describes the ETCD backup, snapshot integrity verification, and offline restore procedure performed in the Kubernetes Production Operations project.

The backup and restore exercise was performed in a KodeKloud multi-node Kubernetes environment.

## Environment

- Kubernetes Version: v1.37.0
- ETCD Version: v3.7.0
- Runtime: containerd
- ETCD Deployment: kubeadm static Pod
- ETCD Node: controlplane

## 1. ETCD Health Verification

ETCD health was checked using `etcdctl`.

```bash
etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  endpoint health
```

The endpoint returned a healthy response.

## 2. ETCD Snapshot Backup

A snapshot was created using ETCDCTL v3.7.0.

Snapshot file:

`etcd-snapshot-2026-11-13-012928.db`

Backup location:

`~/kubernetes-backups/`

The snapshot was approximately 4 MB.

## 3. Snapshot Integrity Verification

The snapshot was inspected using `etcdutl snapshot status`.

The reported snapshot information included:

- Revision: 39882
- Total Keys: 354
- Total Size: approximately 4.1 MB
- ETCD Version: 3.7.0

A SHA256 checksum was generated and verified successfully using `sha256sum -c`.

## 4. Offline Restore Validation

An isolated restore test was performed using `etcdutl`.

```bash
etcdutl snapshot restore /tmp/etcd-snapshot-2026-11-13-012928.db \
  --data-dir=/tmp/etcd-restore-lab \
  --name=restore-lab \
  --initial-cluster=restore-lab=http://127.0.0.1:2380 \
  --initial-advertise-peer-urls=http://127.0.0.1:2380 \
  --initial-cluster-token=restore-lab-token
```

The restore operation completed successfully and created the restored ETCD data directory.

The restored directory contained snapshot and WAL data.

## 5. Post-Restore Cluster Validation

After the offline restore exercise, the original Kubernetes cluster remained healthy.

Validation confirmed:

- All three Kubernetes nodes were Ready.
- ETCD Pod was Running.
- Kubernetes API Server was Running.
- CoreDNS Pods were Running.
- Other Kubernetes system components remained healthy.

**Important:** This exercise validated snapshot restoration into an isolated data directory. It did not perform a live replacement of the production ETCD data directory or a complete cluster disaster recovery.

## 6. Backup Security

ETCD snapshots contain sensitive Kubernetes cluster information, potentially including Kubernetes Secrets.

Therefore:

- Snapshot files must not be committed to public repositories.
- Private keys and certificates must be protected.
- Backup files should be stored in secure external storage.
- Backup integrity should be verified regularly.
- Recovery procedures should be tested in an isolated environment.

## 7. Lab Limitations

The backup file was stored inside the KodeKloud lab environment. Lab storage is temporary and should not be considered durable external backup storage.

A production deployment should copy verified backups to secure external storage.

## Conclusion

ETCD snapshot creation, integrity verification, and isolated offline restoration were successfully validated.

This exercise demonstrates the basic Kubernetes control-plane backup and recovery workflow while highlighting the difference between offline restore validation and complete production disaster recovery.
