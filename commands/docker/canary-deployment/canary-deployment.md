A true **zero-downtime canary deployment with Docker Compose** requires:

1. Multiple versions of the application running simultaneously.
2. A reverse proxy/load balancer (Nginx, Traefik, HAProxy).
3. Traffic splitting (e.g., 90% old version, 10% new version).
4. Health checks.
5. Gradual traffic shifting.
6. Instant rollback.

Since Docker Compose has **no native deployment strategy support** (unlike Kubernetes), the common pattern is:

```text
                     ┌─────────────┐
                     │   Nginx     │
                     │ LoadBalancer│
                     └──────┬──────┘
                            │
            ┌───────────────┼───────────────┐
            │                               │
            ▼                               ▼
      app-v1 (90%)                    app-v2 (10%)
      Stable Version                  Canary Version
```

---

# Project Structure

```text
canary-demo/
│
├── docker-compose.yml
│
├── nginx/
│   ├── nginx.conf
│
├── app-v1/
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
│
└── app-v2/
    ├── Dockerfile
    ├── app.py
    └── requirements.txt
```

---

# Application Version 1

## app-v1/app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return {
        "version": "v1",
        "message": "Stable release"
    }

@app.route("/health")
def health():
    return "OK", 200

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## app-v1/requirements.txt

```text
flask
gunicorn
```

---

## app-v1/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app.py .

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]
```

---

# Application Version 2 (Canary)

## app-v2/app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return {
        "version": "v2",
        "message": "Canary release"
    }

@app.route("/health")
def health():
    return "OK", 200

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## app-v2/requirements.txt

```text
flask
gunicorn
```

---

## app-v2/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app.py .

CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]
```

---

# Nginx Canary Configuration

## nginx/nginx.conf

This sends roughly:

* 90% traffic → v1
* 10% traffic → v2

```nginx
events {}

http {

    upstream stable {
        server app-v1:5000;
    }

    upstream canary {
        server app-v2:5000;
    }

    split_clients "${remote_addr}" $backend {
        90% stable;
        * canary;
    }

    server {
        listen 80;

        location / {

            proxy_pass http://$backend;

            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

            proxy_connect_timeout 5s;
            proxy_read_timeout 30s;
        }
    }
}
```

---

# Docker Compose

## docker-compose.yml

```yaml
version: "3.9"

services:

  app-v1:
    build: ./app-v1
    container_name: app-v1

    healthcheck:
      test: ["CMD", "wget", "--spider", "-q", "http://localhost:5000/health"]
      interval: 10s
      timeout: 3s
      retries: 3

  app-v2:
    build: ./app-v2
    container_name: app-v2

    healthcheck:
      test: ["CMD", "wget", "--spider", "-q", "http://localhost:5000/health"]
      interval: 10s
      timeout: 3s
      retries: 3

  nginx:
    image: nginx:latest
    container_name: nginx

    ports:
      - "80:80"

    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro

    depends_on:
      - app-v1
      - app-v2
```

---

# Start Deployment

```bash
docker compose up -d --build
```

Verify:

```bash
curl http://localhost
```

Output alternates according to traffic split:

```json
{
  "version": "v1",
  "message": "Stable release"
}
```

or

```json
{
  "version": "v2",
  "message": "Canary release"
}
```

---

# Progressive Rollout

## Stage 1

100% v1

```nginx
split_clients "${remote_addr}" $backend {
    100% stable;
}
```

Reload:

```bash
docker exec nginx nginx -s reload
```

---

## Stage 2

95/5

```nginx
split_clients "${remote_addr}" $backend {
    95% stable;
    * canary;
}
```

---

## Stage 3

80/20

```nginx
split_clients "${remote_addr}" $backend {
    80% stable;
    * canary;
}
```

---

## Stage 4

50/50

```nginx
split_clients "${remote_addr}" $backend {
    50% stable;
    * canary;
}
```

---

## Stage 5

100% Canary

```nginx
split_clients "${remote_addr}" $backend {
    100% canary;
}
```

---

# Instant Rollback

If errors appear:

```nginx
split_clients "${remote_addr}" $backend {
    100% stable;
}
```

Reload:

```bash
docker exec nginx nginx -s reload
```

Rollback completes immediately without restarting containers.
