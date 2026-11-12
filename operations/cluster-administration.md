# Kubernetes Cluster Administration

## Project
Kubernetes Production Operations

## Environment
- Kubernetes: v1.37.0
- Nodes: 3
- Control Plane: controlplane
- Workers: node01, node02

## 1. Node Health Assessment

All three nodes were Ready during the administration exercises.

## 2. Cordon and Uncordon

Commands:
- kubectl cordon node02
- kubectl uncordon node02

Results:
- Cordon successfully disabled scheduling on node02.
- Existing DaemonSet pods remained running.
- Uncordon restored scheduling.
- Unschedulable returned to false.

## 3. Node Drain

Command:
kubectl drain node02 --ignore-daemonsets

Results:
- node02 was cordoned automatically.
- DaemonSet-managed Canal and kube-proxy pods were preserved.
- Drain completed successfully.
- node02 was subsequently uncordoned.

## 4. Taint and Toleration

Control plane taint:
node-role.kubernetes.io/control-plane:NoSchedule

### Test 1: Pod Without Toleration

Manifest:
- Pod: test-no-toleration
- Image: nginx:1.27
- Result: Running on node02

The scheduler selected a worker node without the control-plane taint.

### Test 2: Pod With Toleration

Configuration:
- Pod: test-with-toleration
- Image: nginx:1.27
- NodeSelector: control-plane
- Toleration: node-role.kubernetes.io/control-plane
- Effect: NoSchedule
- Result: Running on controlplane

The toleration allowed scheduling onto the tainted control-plane node.
The nodeSelector selected the intended node.

## 5. Cleanup and Final Verification

Both test pods were deleted after successful verification.

Final results:
- 3/3 nodes Ready.
- 13 system pods Running.
- No test pods left behind.
- Control-plane taint unchanged.
- node02 scheduling restored.

## Conclusion

Node administration exercises were completed successfully,
including cordon, uncordon, drain, taint, and toleration.

The cluster returned to its original healthy state.
