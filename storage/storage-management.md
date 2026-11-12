# Kubernetes Storage Management

## Overview

This checkpoint covers Kubernetes persistent storage
using static PersistentVolume and PersistentVolumeClaim
with hostPath storage.

The lab environment does not provide a StorageClass
or CSI driver, so static provisioning was used.

## Environment Assessment

- Kubernetes version: v1.37.0
- Cluster nodes: 3
- StorageClass: Not available
- CSI Drivers: Not available
- PersistentVolumes: Initially none
- PersistentVolumeClaims: Initially none

## PersistentVolume Configuration

Created a static PersistentVolume named `local-pv`.

- Capacity: 1Gi
- Access Mode: ReadWriteOnce
- Reclaim Policy: Retain
- Volume Type: hostPath
- Host Path: /mnt/k8s-storage
- Node Affinity: controlplane

## PersistentVolumeClaim

Created PVC `app-storage` in namespace `storage-lab`.

The PVC successfully bound to `local-pv`.

## Pod Storage Integration

Created Pod `storage-test` using the PVC.

The Pod was scheduled on controlplane because
the hostPath volume is local to that node.

A toleration was added to allow scheduling on
the controlplane node.

The volume was mounted at `/data`.

## Persistence Validation

Created a test file inside the mounted volume:

`/data/persistence-test.txt`

Test content:

`Data survives Pod recreation`

Validation steps:

1. Write data inside the Pod.
2. Read the file successfully.
3. Delete the Pod.
4. Recreate the Pod using the same PVC.
5. Read the file again.

Result: Data remained available after Pod recreation.

## Important Production Considerations

This lab uses hostPath storage for educational purposes.

The storage is local to the controlplane node and
does not provide node-level high availability.

If the node becomes unavailable, workloads depending
on this storage may not be able to access the data.

Production environments should use an appropriate
persistent storage solution, such as CSI-backed
network storage or a supported local persistent volume
configuration.

## Result

Static PersistentVolume and PersistentVolumeClaim
were successfully configured and tested.

Data persistence across Pod recreation was verified.
