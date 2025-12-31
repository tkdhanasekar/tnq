To run **multiple Docker containers (each built from a Dockerfile)** behind a **reverse proxy**, the most common and clean approach is:

👉 **Docker Compose + Nginx (or Traefik) as a reverse proxy**

I’ll explain the **concept**, then give a **working example** using **Nginx**, which is easier to learn.

---

## 1️⃣ High-level idea

* Each app runs in its **own container**
* All containers are on the **same Docker network**
* A **reverse proxy container**:

  * Listens on port 80 (or 443)
  * Routes traffic to containers based on **domain** or **path**

```
Browser
   ↓
Nginx (reverse proxy)
   ↓
App 1 container   App 2 container   App 3 container
```

---

## 2️⃣ Example structure

```
project/
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
├── app1/
│   └── Dockerfile
├── app2/
│   └── Dockerfile
```

---

## 3️⃣ Example apps (simple web servers)

### app1/Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

### app2/Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

Each app just serves a different page.

---

## 4️⃣ Nginx reverse proxy config

### nginx/nginx.conf

```nginx
events {}

http {
    server {
        listen 80;

        location /app1/ {
            proxy_pass http://app1:80/;
        }

        location /app2/ {
            proxy_pass http://app2:80/;
        }
    }
}
```

🔑 **Important**:

* `app1` and `app2` are **service names** (Docker DNS)
* No IP addresses needed

---

## 5️⃣ Docker Compose file (key part)

### docker-compose.yml

```yaml
version: "3.8"

services:
  reverse-proxy:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - app1
      - app2

  app1:
    build: ./app1
    container_name: app1

  app2:
    build: ./app2
    container_name: app2
```

---

## 6️⃣ Run everything

From the project root:

```bash
docker-compose up --build
```

Now visit:

* `http://localhost/app1/`
* `http://localhost/app2/`

🎉 Both containers are running behind **one reverse proxy**

---

## 7️⃣ Domain-based routing (optional)

Instead of paths, you can route by domain:

```nginx
server {
    listen 80;
    server_name app1.localhost;

    location / {
        proxy_pass http://app1:80;
    }
}
```

Then add to `/etc/hosts`:

```
127.0.0.1 app1.localhost
```

---

## 8️⃣ Better alternatives (production)

For real-world projects, consider:

* **Traefik** (auto-discovery, HTTPS)
* **Caddy** (automatic SSL)
* **NGINX + Certbot** (manual SSL)

---

## 9️⃣ Common mistakes

❌ Using `localhost` inside containers
❌ Exposing app ports when using a proxy
❌ Not using the same Docker network
❌ Forgetting trailing slashes in `proxy_pass`

---

If you want, I can:

* Convert this to **Traefik**
* Show **HTTPS with SSL**
* Adapt it for **Node.js / Flask / Spring Boot**
* Explain **how Docker DNS works**

Just tell me 👍

