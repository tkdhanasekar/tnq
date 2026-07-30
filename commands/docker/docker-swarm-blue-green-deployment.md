**Python Flask application** on **Docker Swarm** using a **Blue-Green Deployment** strategy.

---

# Project Structure

```text
flask-bluegreen/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── nginx.conf
└── deploy.sh
```

---

# 1. Flask Application

**app.py**

```python
from flask import Flask
import os

app = Flask(__name__)

VERSION = os.getenv("APP_VERSION", "Blue")

@app.route("/")
def home():
    return f"""
    <h1>Docker Swarm Blue-Green Deployment</h1>
    <h2>Current Version: {VERSION}</h2>
    """

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

# requirements.txt

```text
Flask==3.0.3
gunicorn==22.0.0
```

---

# Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["gunicorn","-b","0.0.0.0:5000","app:app"]
```

---

# Build Images

Blue

```bash
docker build -t flask-app:blue .
```

Green

```bash
docker build -t flask-app:green .
```

---

# Tag

```bash
docker tag flask-app:blue localhost:5000/flask-app:blue

docker tag flask-app:green localhost:5000/flask-app:green
```

---

# 2. Docker Swarm

Initialize Swarm

```bash
docker swarm init
```

---

# 3. Overlay Network

```bash
docker network create \
--driver overlay \
app-network
```

---

# 4. docker-compose.yml

```yaml
version: "3.9"

services:

  blue:
    image: localhost:5000/flask-app:blue
    environment:
      APP_VERSION: BLUE
    deploy:
      replicas: 3
    networks:
      - app-network

  green:
    image: localhost:5000/flask-app:green
    environment:
      APP_VERSION: GREEN
    deploy:
      replicas: 0
    networks:
      - app-network

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    configs:
      - source: nginx_conf
        target: /etc/nginx/nginx.conf
    networks:
      - app-network
    deploy:
      replicas: 1

configs:
  nginx_conf:
    file: ./nginx.conf

networks:
  app-network:
    external: true
```

---

# 5. Nginx Configuration

Initially route traffic to Blue.

```nginx
events {}

http {

upstream backend {
    server blue:5000;
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

# Deploy Stack

```bash
docker stack deploy -c docker-compose.yml flask
```

Verify

```bash
docker service ls
```

---

Expected

```text
flask_blue
flask_green
flask_nginx
```

---

Open

```text
http://localhost
```

Response

```text
Docker Swarm Blue-Green Deployment

Current Version: BLUE
```

---

# Deploy Green Version

Scale Green

```bash
docker service scale flask_green=3
```

Verify

```bash
docker service ps flask_green
```

---

# Switch Traffic

Update `nginx.conf`

```nginx
events {}

http {

upstream backend {
    server green:5000;
}

server {

    listen 80;

    location / {
        proxy_pass http://backend;
    }

}

}
```

Update the Nginx service.

```bash
docker service update --config-rm flask_nginx_conf flask_nginx
```
```
docker config rm flask_nginx_conf
```
```
docker config create flask_nginx_conf nginx.conf
```
```
docker service update --config-rm flask_nginx_conf --config-add source=flask_nginx_conf,target=/etc/nginx/nginx.conf flask_nginx
```

Now users reach:

```text
Current Version: GREEN
```

---

# Remove Blue

```bash
docker service scale flask_blue=0
```

Green becomes the production environment.

---

# Rollback

If Green has issues:

```bash
docker service scale flask_blue=3

docker service scale flask_green=0
```

Change the Nginx upstream back to:

```nginx
upstream backend {
    server blue:5000;
}
```

Reload/update the Nginx configuration.

---

# Automation Script

**deploy.sh**

```bash
#!/bin/bash

ACTIVE=$(docker service ls --format "{{.Name}}" | grep flask_blue)

if [ "$ACTIVE" ]; then

    echo "Deploying GREEN"

    docker service scale flask_green=3

    sleep 20

    cp nginx-green.conf nginx.conf

else

    echo "Deploying BLUE"

    docker service scale flask_blue=3

    sleep 20

    cp nginx-blue.conf nginx.conf

fi

docker config rm flask_nginx_conf 2>/dev/null

docker config create flask_nginx_conf nginx.conf

docker service update \
--config-rm flask_nginx_conf \
--config-add source=flask_nginx_conf,target=/etc/nginx/nginx.conf \
flask_nginx
```

---

# Deployment Flow

```text
                Internet
                    |
              +-------------+
              |    Nginx    |
              +-------------+
                /         \
               /           \
          BLUE             GREEN
      +---------+      +---------+
      Flask x3        Flask x3
      Version A       Version B
```
https://chatgpt.com/s/t_6a69c98a7bf88191964656b469484559
https://chatgpt.com/s/t_6a69d11c57a88191a5cab24fbb539d8e
