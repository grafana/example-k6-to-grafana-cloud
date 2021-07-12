# k6 OSS + Grafana Cloud

This repository contains all the configuration needed to send k6 metrics to your Grafana Cloud
account.

## Prerequisites

- docker
- docker-compose
- credentials for grafana cloud prometheus

## How to use this repository

1. Change `telegraf.conf` to contain your username and password:
```toml
[[outputs.http]]
  url = "https://prometheus-blocks-prod-us-central1.grafana.net/api/prom/push"
  method = "POST"
  username = "YOUR-GRAFANA-CLOUD-PROMETHEUS-USERNAME" # <-- 
  password = "YOUR-GRAFANA-CLOUD-PROMETHEUS-TOKEN"    # <-- 
  data_format = "prometheusremotewrite"
```

2. Start the telegraf container using docker compose
```bash
$ docker compose up -d
```

3. Run your k6 script with the InfluxDB output
```bash
$ k6 run my-test.js -o influxdb
```