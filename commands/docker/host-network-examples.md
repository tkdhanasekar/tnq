Docker Compose examples that use the Docker **host network mode** (`network_mode: host`).

> Note:
>
> * `network_mode: host` works natively on Linux.
> * With host networking, container ports are exposed directly on the host, so you do **not** use the `ports:` section.
> * Containers share the host's network stack.

---

# Example 1: Nginx Web Server

## Directory Structure

```text
nginx-host/
├── docker-compose.yml
├── nginx.conf
└── html/
    └── index.html
```

## docker-compose.yml

```yaml
services:
  nginx:
    image: nginx:latest
    container_name: nginx-host
    network_mode: host
    restart: unless-stopped

    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./html:/usr/share/nginx/html:ro
```

## nginx.conf

```nginx
events {}

http {
    server {
        listen 8080;

        location / {
            root /usr/share/nginx/html;
            index index.html;
        }
    }
}
```

## html/index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Host Network Demo</title>
</head>
<body>
    <h1>Nginx running in host network mode</h1>
</body>
</html>
```

## Run

```bash
docker compose up -d
```

Access:

```text
http://HOST_IP:8080
```

---

# Example 2: Prometheus + Node Exporter

A common monitoring setup where both containers use the host network.

## Directory Structure

```text
monitoring/
├── docker-compose.yml
└── prometheus.yml
```

## docker-compose.yml

```yaml
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    network_mode: host
    restart: unless-stopped

    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml:ro

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    network_mode: host
    restart: unless-stopped

    command:
      - '--path.rootfs=/'
```

## prometheus.yml

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: node-exporter
    static_configs:
      - targets:
          - localhost:9100
```

## Run

```bash
docker compose up -d
```

Access:

```text
http://HOST_IP:9090
```

Node Exporter metrics:

```text
http://HOST_IP:9100/metrics
```

---

# Example 3: Simple Application + Database (Host Network)

If an application must connect to a database via localhost:

```yaml
services:
  postgres:
    image: postgres:16
    container_name: postgres
    network_mode: host
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: appuser
      POSTGRES_PASSWORD: secret

  app:
    image: python:3.12-slim
    container_name: app
    network_mode: host

    command: >
      sh -c "
      pip install psycopg2-binary &&
      python app.py
      "

    volumes:
      - ./app.py:/app.py
```

`app.py`

```python
import psycopg2

conn = psycopg2.connect(
    host="127.0.0.1",
    port=5432,
    dbname="appdb",
    user="appuser",
    password="secret"
)

print("Connected successfully")
```

Since both containers use the host network, the application connects to PostgreSQL through:

```text
127.0.0.1:5432
```

instead of Docker service names.

---

### Verify Host Networking

Start a container:

```bash
docker compose up -d
```

Check network mode:

```bash
docker inspect nginx-host \
  --format '{{.HostConfig.NetworkMode}}'
```

Output:

```text
host
```

Check listening ports directly on the host:

```bash
ss -tulpn
```

or

```bash
netstat -tulpn
```

You should see the container services bound directly to host ports.

