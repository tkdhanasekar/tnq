Docker Compose examples using a **custom bridge network**.

---

# Example 1: Nginx + Web App on a Bridge Network

## Directory Structure

```text
example1/
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
└── app/
    ├── Dockerfile
    └── app.py
```

---

## docker-compose.yml

```yaml
version: "3.9"

services:
  web:
    build: ./app
    container_name: web-app
    networks:
      - backend

  nginx:
    image: nginx:latest
    container_name: nginx-proxy
    ports:
      - "8080:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - web
    networks:
      - backend

networks:
  backend:
    driver: bridge
```

---

## app/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## app/app.py

```python
from http.server import BaseHTTPRequestHandler, HTTPServer

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()
        self.wfile.write(b"Hello from Python container!")

server = HTTPServer(("0.0.0.0", 5000), Handler)
server.serve_forever()
```

---

## nginx/nginx.conf

```nginx
events {}

http {
    upstream backend {
        server web:5000;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
        }
    }
}
```

---

## Run

```bash
docker compose up -d --build
```

Test:

```bash
curl http://localhost:8080
```

Output:

```text
Hello from Python container!
```

---

# Example 2: Application + PostgreSQL on a Bridge Network

This demonstrates service-to-service communication using container DNS.

## Directory Structure

```text
example2/
├── docker-compose.yml
└── app/
    ├── Dockerfile
    ├── requirements.txt
    └── app.py
```

---

## docker-compose.yml

```yaml
version: "3.9"

services:
  postgres:
    image: postgres:16
    container_name: postgres-db
    environment:
      POSTGRES_DB: demo
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret123
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app-network

  app:
    build: ./app
    container_name: python-app
    depends_on:
      - postgres
    environment:
      DB_HOST: postgres
      DB_NAME: demo
      DB_USER: admin
      DB_PASSWORD: secret123
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  postgres_data:
```

---

## app/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

CMD ["python", "app.py"]
```

---

## app/requirements.txt

```text
psycopg2-binary==2.9.10
```

---

## app/app.py

```python
import os
import psycopg2
import time

while True:
    try:
        conn = psycopg2.connect(
            host=os.getenv("DB_HOST"),
            database=os.getenv("DB_NAME"),
            user=os.getenv("DB_USER"),
            password=os.getenv("DB_PASSWORD"),
        )

        cur = conn.cursor()
        cur.execute("SELECT version();")

        print(cur.fetchone())
        cur.close()
        conn.close()

        break

    except Exception as e:
        print("Waiting for database:", e)
        time.sleep(5)
```

---

## Run

```bash
docker compose up -d --build
```

View logs:

```bash
docker logs -f python-app
```

---

## Verify Bridge Network

List networks:

```bash
docker network ls
```

Inspect network:

```bash
docker network inspect example1_backend
```

or

```bash
docker network inspect example2_app-network
```

You will see both containers attached to the same bridge network and able to resolve each other by service name (`web`, `postgres`) through Docker's built-in DNS.

