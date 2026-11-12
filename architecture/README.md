# Kubernetes Architecture

## Overview

This document describes the initial architecture of the Kubernetes
cluster used in the Kubernetes Production Operations project.

The environment consists of one control plane node and two worker nodes.

## Cluster Topology

| Node | Role | Status |
|---|---|---|
| controlplane | Control Plane | Ready |
| node01 | Worker | Ready |
| node02 | Worker | Ready |

## Control Plane Components

- kube-apiserver: Exposes the Kubernetes API.
- etcd: Stores Kubernetes cluster state.
- kube-scheduler: Assigns workloads to suitable nodes.
- kube-controller-manager: Runs cluster controllers.

## Worker Node Components

- kubelet: Communicates with the API Server and manages node workloads.
- kube-proxy: Implements Kubernetes Service networking.
- containerd: Runs application containers.
- Application Pods: Host application workloads.

## Networking Architecture

The cluster uses Canal as its CNI implementation.

- Flannel provides VXLAN-based pod networking.
- Calico provides network policy functionality.
- CoreDNS provides cluster DNS.

## Architecture Diagram

See [cluster-architecture.mmd](diagrams/cluster-architecture.mmd).

## Architecture Limitations

This environment has a single control plane node.
Therefore, it does not provide control plane high availability.

This is a learning and production-operations simulation environment,
not a production HA deployment.
