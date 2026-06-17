**Docker Compose examples using a Docker Overlay Network**. Overlay networks require **Docker Swarm mode** (`docker swarm init`) because they span multiple Docker hosts.

---

# Example 1: Two Services Communicating Over an Overlay Network

## Directory Structure

```text
example1/
├── docker-compose.yml
└── app/
    └── index.html
```

## Initialize Swarm

```bash
docker swarm init
```

## docker-compose.yml

```yaml
version: "3.9"

services:
  web:
    image: nginx:alpine
    ports:
      - "8080:80"
    networks:
      - app-overlay
    deploy:
      replicas: 2

  api:
    image: hashicorp/http-echo
    command:
      - "-text=Hello from API Service"
    networks:
      - app-overlay
    deploy:
      replicas: 2

networks:
  app-overlay:
    driver: overlay
    attachable: true
```

## Deploy Stack

```bash
docker stack deploy -c docker-compose.yml demo
```

## Verify

List networks:

```bash
docker network ls
```

Check services:

```bash
docker service ls
```

Inspect overlay network:

```bash
docker network inspect demo_app-overlay
```

Remove stack:

```bash
docker stack rm demo
```

---

# Example 2: Multi-Host Overlay Network with PostgreSQL and Application

This example simulates a typical microservice deployment where an application accesses PostgreSQL through an overlay network.

## Directory Structure

```text
example2/
├── docker-compose.yml
└── app/
    ├── Dockerfile
    └── app.py
```

---

## app/app.py

```python
import os
import psycopg2
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    conn = psycopg2.connect(
        host=os.environ["DB_HOST"],
        database=os.environ["DB_NAME"],
        user=os.environ["DB_USER"],
        password=os.environ["DB_PASSWORD"]
    )

    cur = conn.cursor()
    cur.execute("SELECT version();")
    version = cur.fetchone()

    cur.close()
    conn.close()

    return f"Connected to PostgreSQL: {version[0]}"

app.run(host="0.0.0.0", port=5000)
```

---

## app/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

RUN pip install flask psycopg2-binary

COPY app.py .

CMD ["python", "app.py"]
```

---

## docker-compose.yml

```yaml
version: "3.9"

services:
  postgres:
    image: postgres:16
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: appuser
      POSTGRES_PASSWORD: secret123
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - backend-overlay
    deploy:
      replicas: 1

  app:
    build: ./app
    ports:
      - "5000:5000"
    environment:
      DB_HOST: postgres
      DB_NAME: appdb
      DB_USER: appuser
      DB_PASSWORD: secret123
    networks:
      - backend-overlay
    deploy:
      replicas: 2

networks:
  backend-overlay:
    driver: overlay
    attachable: true

volumes:
  pgdata:
```

---

## Deploy

```bash
docker swarm init

docker stack deploy -c docker-compose.yml myapp
```

## Scale Application

```bash
docker service scale myapp_app=5
```

## Test

```bash
curl http://localhost:5000
```

Expected output:

```text
Connected to PostgreSQL: PostgreSQL 16.x ...
```

---

# Multi-Node Swarm Setup (Required for Real Overlay Networking)

### Manager Node

```bash
docker swarm init --advertise-addr <MANAGER-IP>
```

Get join token:

```bash
docker swarm join-token worker
```

### Worker Node

```bash
docker swarm join \
  --token <TOKEN> \
  <MANAGER-IP>:2377
```

Verify:

```bash
docker node ls
```

Once nodes join the swarm, services attached to the overlay network can communicate across hosts using Docker's built-in DNS (service names such as `postgres`, `api`, `web`, etc.).

