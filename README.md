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
1. Fetches Metrics from HTTP endpoints(...port/metrics), By default, this is the /metrics path. You can customize the path using the metrics_path setting in prometheus.yml.
2. Stores Metrics in Time Series Database (TSDB). Each data point is stored with a timestamp, metric name, and labels (key-value pairs).
3. Provides PromQL for Querying: Prometheus uses PromQL (Prometheus Query Language) to query stored metrics.

🔄 How Data Becomes Available at /metrics
1. Exporters Fetch data from systems
2. Convert into Prometheus exposition format.
3. Expose at /metrics endpoint.

📦 Common Exporters
node_exporter	Host-level metrics (CPU, memory)
cadvisor	Container metrics (Docker, Kubernetes)
blackbox_exporter	Ping/HTTP checks
mysqld_exporter	MySQL metrics
nginx_exporter	NGINX metrics
kube-state-metrics	Kubernetes object states

```
