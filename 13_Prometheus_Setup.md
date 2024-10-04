# Install Prometheus and cAdvisor
  
- cAdvisor (short for container Advisor) analyzes and exposes resource usage and performance data from running containers. cAdvisor exposes Prometheus metrics out of the box.

- Download the prometheus config file
```
wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
```
## Install Prometheus using Docker
```
docker run -d --name=prometheus -p 9090:9090 -v <PATH_TO_prometheus.yml_FILE>:/etc/prometheus/prometheus.yml prom/prometheus --config.file=/etc/prometheus/prometheus.yml
```

## Add cAdvisor target

```
scrape_configs:
- job_name: cadvisor
  scrape_interval: 5s
  static_configs:
  - targets:
    - cadvisor:8080
```

### Using Docker Compose

```
version: '3.2'
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
    - 9090:9090
    command:
    - --config.file=/etc/prometheus/prometheus.yml
    volumes:
    - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro
    depends_on:
    - cadvisor
  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    container_name: cadvisor
    ports:
    - 8080:8080
    volumes:
    - /:/rootfs:ro
    - /var/run:/var/run:rw
    - /sys:/sys:ro
    - /var/lib/docker/:/var/lib/docker:ro
    depends_on:
    - redis
  redis:
    image: redis:latest
    container_name: redis
    ports:
    - 6379:6379
```
###  Verify
```
docker-compose up -d
docker-compose ps

Test PromQL
rate(container_cpu_usage_seconds_total{name="redis"}[1m])
container_memory_usage_bytes{name="redis"}
```
