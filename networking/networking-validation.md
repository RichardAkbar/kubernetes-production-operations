# Kubernetes Networking & CNI Validation

## Environment
- Kubernetes Version: v1.37.0
- CNI: Canal
- Networking Backend: Flannel VXLAN
- Network Policy: Calico
- DNS: CoreDNS

## 1. Initial Network Assessment

- Canal pods: 3/3 Running
- CoreDNS pods: 2/2 Running
- Initial NetworkPolicies: None

## 2. Cross-Node Pod Communication

Test namespace: networking-lab

| Pod | IP Address | Node |
|---|---|---|
| network-client | 172.17.1.2 | node01 |
| nginx-server | 172.17.2.3 | node02 |

Test:
HTTP request from network-client to nginx-server Pod IP.

Result:
HTTP/1.1 200 OK

Conclusion:
Cross-node Pod communication works successfully.

## 3. Kubernetes DNS Validation

DNS Server:
172.20.0.10

Test 1:
kubernetes.default.svc.cluster.local

Resolved IP:
172.20.0.1

Test 2:
kube-dns.kube-system.svc.cluster.local

Resolved IP:
172.20.0.10

Conclusion:
CoreDNS successfully resolves Kubernetes internal DNS records.

## 4. ClusterIP Service Validation

Service:
- Name: nginx-service
- Namespace: networking-lab
- Type: ClusterIP
- ClusterIP: 172.20.134.186
- Port: 80/TCP
- Endpoint: 172.17.2.3:80

Test:
HTTP request using nginx-service.networking-lab.svc.cluster.local

Result:
HTTP/1.1 200 OK

Conclusion:
Kubernetes Service discovery and ClusterIP routing work successfully.

## 5. Calico NetworkPolicy Validation

Policy:
allow-nginx-from-approved-client

Selected Pod:
app=nginx-server

Allowed ingress:
- Source label: role=allowed-client
- Protocol: TCP
- Port: 80

### Allowed Client Test

Pod:
network-client

Label:
role=allowed-client

Result:
HTTP/1.1 200 OK

### Denied Client Test

Pod:
test-client-denied

Label:
No matching allowed-client label

Result:
Connection timed out.

Conclusion:
NetworkPolicy successfully restricts ingress traffic to
the selected NGINX Pod.

## 6. Cleanup and Final Health

- test-client-denied deleted.
- network-client remains Running.
- nginx-server remains Running.
- nginx-service remains available.
- NetworkPolicy remains active.
- All 3 Kubernetes nodes remain Ready.

## Conclusion

Cross-node networking, Kubernetes DNS, ClusterIP Service
discovery, and Calico NetworkPolicy were successfully validated.
