
# Kubernetes Monitoring and Observability

## Overview

This document describes the implementation and validation of Kubernetes monitoring and observability using Prometheus and Grafana.

The monitoring stack was deployed using Helm in a KodeKloud multi-node Kubernetes environment.

## Environment

- Kubernetes: v1.37.0
- Helm: v3.22.1
- Monitoring Chart: kube-prometheus-stack
- Chart Version: 93.2.2
- Prometheus App Version: v3.16.0
- Grafana: kube-prometheus-stack bundled Grafana
- Namespace: monitoring

## 1. Monitoring Architecture

The monitoring stack consists of:

- Prometheus: metrics collection and querying
- Grafana: metrics visualization and dashboards
- Alertmanager: alert management
- Prometheus Operator: monitoring resource management
- kube-state-metrics: Kubernetes object state metrics

Node Exporter was disabled because its host filesystem mount configuration was incompatible with the KodeKloud Playground environment.

## 2. Helm Repository

Prometheus Community Helm repository was added:

```bash
helm repo add prometheus-community \
  https://prometheus-community.github.io/helm-charts

helm repo update
```

The kube-prometheus-stack chart version 93.2.2 was selected.

## 3. Monitoring Configuration

The monitoring configuration is stored in:

`monitoring-values.yaml`

Key configuration:

- Grafana persistence disabled
- Prometheus storageSpec left empty
- Alertmanager storage left empty
- Node Exporter disabled

Persistent storage was not configured because the Kubernetes environment did not provide a StorageClass.

This configuration is intended for an ephemeral lab environment, not durable production monitoring storage.

## 4. Installation

The monitoring stack was installed using Helm:

```bash
helm upgrade --install monitoring \
  prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --version 93.2.2 \
  -f monitoring-values.yaml
```

The Helm release reached the `deployed` status.

## 5. Kubernetes Resources

The monitoring namespace contains:

- Prometheus
- Grafana
- Alertmanager
- Prometheus Operator
- kube-state-metrics

The monitoring services use ClusterIP networking.

Grafana and Prometheus were accessed using Kubernetes port-forwarding.

## 6. Grafana Validation

Grafana was accessed through port-forwarding:

```bash
kubectl port-forward \
  --address 0.0.0.0 \
  -n monitoring \
  svc/monitoring-grafana 3000:80
```

The Kubernetes Compute Resources / Cluster dashboard was validated.

Observed metrics included:

- CPU usage by namespace
- Memory usage by namespace
- CPU requests commitment
- Memory requests commitment
- Namespace and Pod resource information

The dashboard displayed metrics for the `kube-system` and `monitoring` namespaces.

Some host-level utilization panels displayed No data because Node Exporter was disabled.

## 7. Prometheus Target Validation

Prometheus was accessed through port-forwarding:

```bash
kubectl port-forward \
  --address 0.0.0.0 \
  -n monitoring \
  svc/monitoring-kube-prometheus-prometheus 9090:9090
```

The Prometheus Targets page showed successful scraping for several monitoring endpoints, including:

- Grafana
- Alertmanager
- Kubernetes API Server
- CoreDNS
- Kubelet

The PromQL query used for validation:

```promql
up
```

The query returned 28 time series.

Target health summary at the time of validation:

| Metric | Result |
|---|---:|
| Targets UP | 19 |
| Targets DOWN | 9 |
| Total targets | 28 |
| UP percentage | 67.86% |

The following aggregate queries were also executed:

```promql
count(up == 1)
```

Result: 19

```promql
count(up == 0)
```

Result: 9

Some targets, including kube-controller-manager, kube-proxy, and etcd, returned a value of 0 during validation.

These results represent the observed state of the lab environment at the time of testing.

## 8. Environment Limitations

The following limitations were identified:

1. No StorageClass was available.
2. Prometheus and Grafana used non-persistent storage configuration.
3. Node Exporter was disabled because of host mount propagation restrictions.
4. Some Kubernetes component scrape targets were unavailable.
5. The monitoring environment is temporary and tied to the KodeKloud lab lifecycle.

A production implementation should use durable storage, secure external access, and complete monitoring coverage.

## 9. Security Considerations

- Grafana credentials must be stored securely.
- Do not commit passwords or Kubernetes secrets to Git.
- Use appropriate authentication and network restrictions.
- Avoid exposing administrative dashboards publicly.
- Use persistent and protected storage for production monitoring data.

## Conclusion

Prometheus and Grafana were successfully deployed and validated in the Kubernetes cluster.

Grafana displayed Kubernetes resource metrics, while Prometheus successfully collected metrics from multiple cluster components.

The monitoring implementation demonstrates Kubernetes observability fundamentals and documents the limitations encountered in the lab environment.
