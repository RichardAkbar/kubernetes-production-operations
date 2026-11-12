# Kubernetes Cluster Architecture

## Project Information
- Project: Kubernetes Production Operations
- Owner: Richard Jabarul Akbar
- Environment: KodeKloud Playground
- Kubernetes Version: v1.37.0

## Cluster Topology

| Node | Role | Status |
|---|---|---|
| controlplane | Control Plane | Ready |
| node01 | Worker | Ready |
| node02 | Worker | Ready |

## Control Plane Components
- kube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager

## Worker Node Components
- kubelet
- kube-proxy
- containerd
- Canal CNI

## Networking
- CNI: Canal
- Backend: Flannel VXLAN
- Network Policy: Calico
- DNS: CoreDNS

## Pod CIDR
- controlplane: 172.17.0.0/24
- node01: 172.17.1.0/24
- node02: 172.17.2.0/24

## Scheduling
- Control Plane: NoSchedule taint
- node01: Schedulable
- node02: Schedulable

## Architecture Type
Single Control Plane with Two Worker Nodes.

## Architecture Notes
This environment is a Kubernetes learning and production-operations
simulation. It is not a highly available production cluster because
it has only one control-plane node.
