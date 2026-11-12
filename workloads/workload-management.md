
# Kubernetes Workload Management

## Environment
- Kubernetes Version: v1.37.0
- Namespace: workload-lab
- Application: NGINX
- Container Image: nginx:1.27
- Replicas: 5

## 1. Deployment and ReplicaSet

Created an NGINX Deployment with 3 initial replicas.

Deployment:
- Name: nginx-deployment
- Namespace: workload-lab
- Image: nginx:1.27

Kubernetes automatically created a ReplicaSet to maintain the desired number of Pods.

## 2. Scaling

Scaled the Deployment from 3 to 5 replicas.

Command:
`kubectl scale deployment nginx-deployment --replicas=5 -n workload-lab`

Result:
- Desired replicas: 5
- Current replicas: 5
- Ready replicas: 5

The scheduler distributed the Pods across worker nodes.

## 3. Rolling Update

Updated the container image from nginx:1.27 to nginx:1.28.

Command:
`kubectl set image deployment/nginx-deployment nginx=nginx:1.28 -n workload-lab`

Result:
- New ReplicaSet created.
- Old ReplicaSet scaled down to zero.
- New ReplicaSet reached 5 ready replicas.
- Deployment remained available.

Strategy:
- RollingUpdate
- MaxUnavailable: 25%
- MaxSurge: 25%

## 4. Rollback

Performed a rollback to the previous Deployment revision.

Command:
`kubectl rollout undo deployment/nginx-deployment -n workload-lab`

Result:
- Image restored to nginx:1.27.
- Deployment successfully rolled out.
- All 5 replicas became available.

## 5. Liveness Probe

Configured an HTTP GET liveness probe on path `/`.

A separate test Deployment used the invalid path `/healthz`.

Result:
- HTTP 404 returned by NGINX.
- Liveness probe failed repeatedly.
- Kubelet restarted the container.
- Restart count increased.

This validated automatic container recovery.

## 6. Readiness Probe

Configured an HTTP GET readiness probe on path `/`.

A separate test Deployment used the invalid path `/readyz`.

Result:
- Pod remained Running.
- Pod readiness became False (0/1).
- Container restart count remained 0.
- Readiness probe reported HTTP 404.

This validated that an unready Pod is not considered available for Service traffic.

## 7. Resource Requests and Limits

Final container resource configuration:

| Resource | Request | Limit |
|---|---|---|
| CPU | 100m | 500m |
| Memory | 128Mi | 256Mi |

Requests define the resources used for scheduling. Limits define the maximum resource consumption allowed for the container.

## 8. Final Deployment Configuration

- Deployment: nginx-deployment
- Namespace: workload-lab
- Image: nginx:1.27
- Replicas: 5
- Liveness Probe: HTTP GET /
- Readiness Probe: HTTP GET /
- CPU Request: 100m
- CPU Limit: 500m
- Memory Request: 128Mi
- Memory Limit: 256Mi

## 9. Final Health Verification

- Deployment: 5/5 Ready
- Active ReplicaSet: 5/5 Ready
- Running Pods: 5
- Pod restarts: 0
- Worker nodes: node01 and node02
- Previous ReplicaSets retained with zero replicas.

## Conclusion

Deployment management, ReplicaSet behavior, horizontal scaling, rolling updates, rollback, health probes, and container resource management were successfully practiced and validated.
