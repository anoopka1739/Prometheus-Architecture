Prometheus Architecture Deep Dive (kube-prometheus-stack using Helm)

To monitor our software systems and infrastructure load, we can use Prometheus to fetch and store metrics.
Now, to deploy Prometheus in our Kubernetes cluster, we use Helm charts.

Prometheus is an industry-standard monitoring tool, and it's commonly deployed using the popular kube-prometheus-stack.
The kube-prometheus-stack contains all the manifests and configuration files required to deploy monitoring services efficiently.

The kube-prometheus-stack includes multiple components:
Prometheus Operator:
-- It is responsible for managing Prometheus instances using Kubernetes Custom Resource Definitions (CRDs).
-- This extends the Kubernetes API server to support Prometheus-specific resources.

ServiceMonitor:
-- This is a critical component—it exposes application metrics to the Prometheus server.
-- Prometheus can then scrape these metrics and store them in its time-series database.
-- We can define multiple targets and expose them via ServiceMonitor, which is a Custom Resource created by the Prometheus Operator.

Alertmanager:
-- Integrated into the stack, it’s configured to trigger alerts based on defined thresholds or unusual events.

PrometheusRule:
-- All alerting and recording rules are defined here.

To collect metrics from various components, kube-prometheus-stack includes:

1. Node Exporter (Node Monitoring):
--> Fetches system-level metrics (CPU, memory, disk, etc.) from each node and stores them in Prometheus.

2. kube-state-metrics (Infrastructure Monitoring):
--> Monitors the state of Kubernetes resources such as Pods, Deployments, and Services.
These metrics are also stored in the Prometheus database.

3. Application Monitoring:
--> Every application can export Prometheus-compatible metrics, usually to the "/metrics" endpoint.
These can be added as scrape targets using ServiceMonitor.

All the above three components can be added as monitoring targets.
Finally, the Prometheus database stores all collected metrics, which are visualized using Grafana to monitor performance, health, and availability in real time.
