# Grafana and Prometheus

> Some monitoring experiments with Grafana and Prometheus.

## About

#### Requirements

- **[Docker](https://www.docker.com/)** working in your machine.
- **[docker-compose](https://docs.docker.com/compose/)** already installed.

## Quick start

```bash
# Clone the repository
git clone https://github.com/lucianocarvalho/grafana-prometheus.git && cd grafana-prometheus

# Setup the containers
docker-compose up -d
```

To open node exporter metrics, go to **[http://localhost:9100/metrics](http://localhost:9100/metrics)**.

To open Prometheus, go to **[http://localhost:9090/](http://localhost:9090/)**.

To open Grafana, go to **[http://localhost:3000/](http://localhost:3000/)** (login admin/admin).