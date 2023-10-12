# Prometheus Installation On Ubuntu (Any Linux variant is also fine)
## Go to [Prometheus Downloads](https://prometheus.io/download/) and download the latest version available at that time

    wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz

## Extract the files and change to the directory

    tar xvzf prometheus-2.47.1.linux-amd64.tar.gz
    cd prometheus-2.47.1.linux-amd64

## Delete or rename existing config file prometheus.yml file and ensure that the below contents are added

```
global:
scrape_interval:     15s # By default, scrape targets every 15 seconds.

# Attach these labels to any time series or alerts when communicating with
# external systems (federation, remote storage, Alertmanager).
external_labels:
    monitor: 'codelab-monitor'

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
# The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
- job_name: 'prometheus'

    # Override the global default and scrape targets from this job every 5 seconds.
    scrape_interval: 5s

    static_configs:
    - targets: ['localhost:9090']
```
