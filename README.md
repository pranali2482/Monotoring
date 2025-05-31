```
[ Application/Server ]
     ↓
[ Exporter or Code Instrumention or Pushgateway ]
     ↓
  Exposes metrics at /metrics
     ↓
[ Prometheus scrapes /metrics periodically from http endpoints]
     ↓
[ Stores in TSDB ]
     ↓
[ Query using PromQL → Dashboard or Alerts ]

✅ Prometheus: How It Works?
1. Scrapes Metrics from HTTP endpoints(...port/metrics), default path is /metrics. You can customize the path using the metrics_path setting in prometheus.yml.
2. Stores Metrics in Time Series Database (TSDB). Each data point is stored with a timestamp, metric name, and labels (key-value pairs).
3. Provides PromQL for Querying: Prometheus uses PromQL (Prometheus Query Language) to query stored metrics.

Prometheus uses the prometheus.yml file to know about: What metrics to collects, targets, timestamp to scrap metrics, configuring alerts etc.
a. Installing Standalone Prometheus: You provide and manage the prometheus.yml file yourself.
b. Installing Prometheus on Kubernetes using kube-prometheus-stack: Direct editing of prometheus.yml is not allowed,
managed declaratively via Kubernetes resources like Servicemonitor, Podmonitor, Prometheusrule etc.
The Operator watches for these resources and updates the Prometheus configuration automatically.


🔄 How Data Becomes Available at /metrics
1. Fetches metrics from systems or servers.
2. Convert into Prometheus exposition format.
3. Expose/make available at /metrics endpoint.

📦 Common Exporters
node_exporter: Host-level metrics (CPU, memory)
kube-state-metrics: Kubernetes object states
cadvisor: Container metrics (Docker, Kubernetes)
blackbox_exporter: Ping/HTTP checks
mysqld_exporter: MySQL metrics
nginx_exporter: NGINX metrics

##Complete Prometheus monitoring solution for Kubernetes:
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace

Kube-Prometheus Stack (Recommended): Includes: Prometheus + Grafana + Alertmanager + Node Exporter + Kube-State-Metrics +
Prometheus Operator(Manages Prometheus using CRDs (ServiceMonitor, PrometheusRule)).

| Component     | Deployed As | Runs Where    | Role                         |
| ------------- | ----------- | ------------- | ---------------------------- |
| Prometheus    | Pod         | monitoring ns | Scrape and store metrics     |
| Grafana       | Pod         | monitoring ns | Dashboard and alerting UI    |
| Node Exporter | DaemonSet   | All K8s nodes | Collect system-level metrics |
| App Exporters | Pod         | Same app ns   | Collect app-level metrics    |
| Pushgateway   | Pod         | monitoring ns | For short-lived jobs         |

```
