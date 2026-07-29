**production-style Python Flask application** deployed on **Docker Swarm** using a **Blue-Green Deployment Strategy**.

This example includes:

```
blue-green-swarm/
│
├── app/
│   ├── app.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── version.txt
│
├── nginx/
│   ├── nginx.conf
│   ├── blue.conf
│   └── green.conf
│
├── stack-blue.yml
├── stack-green.yml
├── deploy-blue.sh
├── deploy-green.sh
├── switch-blue.sh
├── switch-green.sh
└── README.md
```

---

# 1. Flask Application

## app/app.py

```python
from flask import Flask
import socket
import os

app = Flask(__name__)

VERSION = "Unknown"

if os.path.exists("version.txt"):
    with open("version.txt") as f:
        VERSION = f.read().strip()


@app.route("/")
def home():
    return {
        "Application": "Docker Swarm Blue-Green Demo",
        "Version": VERSION,
        "Hostname": socket.gethostname()
    }


@app.route("/health")
def health():
    return "OK"


if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## app/version.txt

Blue

Later change to

```
Green
```

---

## app/requirements.txt

```
Flask==3.0.2
gunicorn==22.0.0
```

---

## app/Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["gunicorn","-w","4","-b","0.0.0.0:5000","app:app"]
```

---

# 2. Reverse Proxy

## nginx/nginx.conf

```nginx
events {}

http {

include /etc/nginx/conf.d/default.conf;

}
```

---

## nginx/blue.conf

```nginx
server {

    listen 80;

    location / {

        proxy_pass http://blue_app:5000;

        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    }

}
```

---

## nginx/green.conf

```nginx
server {

    listen 80;

    location / {

        proxy_pass http://green_app:5000;

        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

    }

}
```

---

# 3. Blue Stack

## stack-blue.yml

```yaml
version: "3.9"

services:

  blue_app:
    image: flask-blue:v1
    deploy:
      replicas: 3

    networks:
      - app_net

  nginx:
    image: nginx:latest

    ports:
      - "80:80"

    configs:
      - source: blue_conf
        target: /etc/nginx/conf.d/default.conf

    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf

    networks:
      - app_net

configs:

  blue_conf:
    file: ./nginx/blue.conf

networks:

  app_net:
```

---

# 4. Green Stack

## stack-green.yml

```yaml
version: "3.9"

services:

  green_app:

    image: flask-green:v2

    deploy:

      replicas: 3

    networks:

      - app_net

  nginx:

    image: nginx:latest

    ports:

      - "80:80"

    configs:

      - source: green_conf
        target: /etc/nginx/conf.d/default.conf

    volumes:

      - ./nginx/nginx.conf:/etc/nginx/nginx.conf

    networks:

      - app_net

configs:

  green_conf:

    file: ./nginx/green.conf

networks:

  app_net:
```

---

# 5. Build Images

Blue

```bash
docker build -t flask-blue:v1 app/
```

Green

Edit

```
version.txt

Blue
```

to

```
Green
```

then

```bash
docker build -t flask-green:v2 app/
```

---

# 6. Initialize Swarm

```bash
docker swarm init
```

---

# 7. Deploy Blue

```bash
docker stack deploy -c stack-blue.yml blue
```

Verify

```bash
curl http://localhost
```

Output

```json
{
  "Application":"Docker Swarm Blue-Green Demo",
  "Version":"Blue",
  "Hostname":"blue_app.1.xxxxxx"
}
```

---

# 8. Deploy Green

```bash
docker stack deploy -c stack-green.yml green
```

Green is now running but not serving production traffic if your routing still points to Blue.

---

# 9. Switch Traffic

Blue

```
NGINX
      |
      |
  Blue Service
```

Green

Replace

```
blue.conf
```

with

```
green.conf
```

Reload nginx

```bash
docker service update \
--config-rm blue_blue_conf \
--config-add source=green_green_conf,target=/etc/nginx/conf.d/default.conf \
blue_nginx
```

or simply redeploy

```bash
docker stack deploy -c stack-green.yml green
```

Now

```bash
curl localhost
```

returns

```json
{
 "Version":"Green"
}
```

---

# 10. Rollback

If Green fails

```bash
docker stack rm green
```

Traffic remains on Blue.

---

# 11. Deployment Scripts

## deploy-blue.sh

```bash
#!/bin/bash

docker build -t flask-blue:v1 app/

docker stack deploy -c stack-blue.yml blue
```

---

## deploy-green.sh

```bash
#!/bin/bash

docker build -t flask-green:v2 app/

docker stack deploy -c stack-green.yml green
```

---

## switch-blue.sh

```bash
#!/bin/bash

docker stack deploy -c stack-blue.yml blue
```

---

## switch-green.sh

```bash
#!/bin/bash

docker stack deploy -c stack-green.yml green
```

---

# 12. Check Swarm

```bash
docker node ls

docker service ls

docker stack ls

docker service ps blue_blue_app

docker service ps green_green_app
```

---

# 13. Scale

```bash
docker service scale blue_blue_app=5
```

or

```bash
docker service scale green_green_app=5
```

---

# 14. Rolling Update

```bash
docker service update \
--image flask-green:v3 \
green_green_app
```

---

# 15. Rollback

```bash
docker service rollback green_green_app
```

---
