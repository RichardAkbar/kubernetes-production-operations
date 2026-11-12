# Kubernetes Production Operations

## 1. Overview

This section documents production-oriented Kubernetes operations, including cluster health assessment, workload troubleshooting, resource capacity analysis, and workload self-healing.

The activities were performed on a three-node Kubernetes cluster using Kubernetes v1.37.0.

## 2. Cluster Health Assessment

### Node Status

The cluster consists of three nodes:

- controlplane
- node01
- node02

All nodes reported `Ready` status during the assessment.

### System Components

The following Kubernetes components were verified:

- kube-apiserver
- kube-controller-manager
- kube-scheduler
- etcd
- CoreDNS
- kube-proxy
- Canal CNI

System Pods were running successfully during the assessment.

### Pod and Event Inspection

Commands used:

```bash
kubectl get pods -A -o wide
kubectl get pods -n kube-system
kubectl get events -A --sort-by=.metadata.creationTimestamp
kubectl describe nodes
```

These commands help identify unhealthy workloads, scheduling issues, node conditions, and Kubernetes events.

## 3. ImagePullBackOff Troubleshooting

### Problem

A test Pod named `broken-nginx` was deployed with an invalid container image:

```yaml
image: nginx:999.999.invalid
```

The Pod entered `ImagePullBackOff`.

### Investigation

```bash
kubectl describe pod broken-nginx -n troubleshooting-lab
```

The events showed image pull failures and `ErrImagePull`.

### Root Cause

The specified container image tag did not exist.

### Resolution

The image was changed to:

```yaml
image: nginx:1.27
```

The Pod returned to `Running` status.

### Verification

```bash
kubectl get pods -n troubleshooting-lab
kubectl logs broken-nginx -n troubleshooting-lab
```

An HTTP request from a separate client Pod to the NGINX Pod IP returned HTTP 200 OK.

## 4. CrashLoopBackOff Troubleshooting

### Problem

A test container was configured to exit with a non-zero status:

```yaml
command: ["sh", "-c", "echo Application starting...; exit 1"]
```

The Pod repeatedly restarted and entered `CrashLoopBackOff`.

### Investigation

```bash
kubectl describe pod crashloop-demo -n troubleshooting-lab
kubectl logs crashloop-demo -n troubleshooting-lab
```

The logs showed:

```text
Application starting...
```

The Pod events showed repeated container restarts and `BackOff`.

### Root Cause

The container process exited with status code 1.

### Resolution

The container command was changed to:

```yaml
command: ["sh", "-c", "echo Application recovered; sleep 3600"]
```

The Pod was deleted and recreated using the corrected manifest.

### Verification

The Pod returned to:

- Status: Running
- Ready: True
- Restart Count: 0

The application log showed:

```text
Application recovered
```

## 5. Resource Monitoring and Capacity Planning

### Metrics API Availability

The following commands were executed:

```bash
kubectl top nodes
kubectl top pods -A
kubectl get apiservices | grep metrics
```

The `kubectl top` commands returned:

```text
error: Metrics API not available
```

No Metrics APIService was listed.

Therefore, actual CPU and memory utilization could not be collected through Kubernetes Metrics API during this lab.

### Node Capacity

Node capacity was inspected using:

```bash
kubectl describe nodes
```

Each node provided approximately:

- 16 CPU cores
- 61.9 GiB memory

### Allocated Resources

Scheduler resource requests and limits were inspected for each node.

These values represent scheduled resource allocation, not actual runtime utilization.

### Workload Resource Requests and Limits

The NGINX Deployment contains five replicas.

Each Pod is configured with:

| Resource | Request | Limit |
|---|---:|---:|
| CPU | 100m | 500m |
| Memory | 128Mi | 256Mi |

Total configured resources for five replicas:

- CPU request: 500m
- CPU limit: 2500m
- Memory request: 640Mi
- Memory limit: 1280Mi

## 6. Deployment Self-Healing

### Objective

Verify whether Kubernetes automatically replaces a deleted Pod managed by a Deployment.

### Test

One Pod from the `nginx-deployment` Deployment was manually deleted.

```bash
kubectl delete pod <pod-name> -n workload-lab
```

### Observation

The ReplicaSet detected that the number of available Pods had decreased and created a replacement Pod.

The replacement Pod received a new name and successfully reached `Running` status.

### Verification

```bash
kubectl get deployment nginx-deployment -n workload-lab
kubectl get pods -n workload-lab
kubectl get replicasets -n workload-lab
```

Final Deployment status:

- Desired replicas: 5
- Ready replicas: 5
- Available replicas: 5

This confirms successful Deployment self-healing.

## 7. Operational Findings

The production operations exercises confirmed:

1. Cluster nodes and system components were healthy during assessment.
2. Invalid container images can cause `ImagePullBackOff`.
3. Applications that exit repeatedly can cause `CrashLoopBackOff`.
4. Container logs and Pod events are essential troubleshooting tools.
5. Resource requests and limits help define workload resource allocation.
6. Metrics API was unavailable in the lab, preventing actual CPU and memory utilization monitoring.
7. Kubernetes Deployments automatically replace deleted Pods through ReplicaSets.

## 8. Conclusion

The Kubernetes production operations exercises were completed successfully.

Cluster health inspection, workload troubleshooting, resource capacity analysis, and Deployment self-healing were tested and documented.

The environment demonstrated core Kubernetes operational capabilities while also identifying monitoring limitations that should be addressed in a production environment.
