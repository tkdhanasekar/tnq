Below is the **same setup converted to Traefik**, using **Docker Compose**, with **automatic routing** and **no manual proxy config files**.

This is the **recommended modern approach**.

---

## 1️⃣ Why Traefik?

✔ No Nginx config files
✔ Auto-discovers containers
✔ Clean labels-based routing
✔ Easy HTTPS later
✔ Perfect for multiple Dockerfiles

---

## 2️⃣ Project structure (simpler)

```
project/
├── docker-compose.yml
├── app1/
│   └── Dockerfile
├── app2/
│   └── Dockerfile
```

No Traefik config file needed for basic usage.

---

## 3️⃣ App Dockerfiles (same as before)

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

---

## 4️⃣ Docker Compose with Traefik

### docker-compose.yml

```yaml
version: "3.9"

services:
  traefik:
    image: traefik:v3.0
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.web.address=:80"
    ports:
      - "80:80"
      - "8080:8080" # Traefik dashboard
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro

  app1:
    build: ./app1
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.app1.rule=PathPrefix(`/app1`)"
      - "traefik.http.services.app1.loadbalancer.server.port=80"

  app2:
    build: ./app2
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.app2.rule=PathPrefix(`/app2`)"
      - "traefik.http.services.app2.loadbalancer.server.port=80"
```

---

## 5️⃣ Run it

```bash
docker-compose up --build
```

Open:

* `http://localhost/app1`
* `http://localhost/app2`
* `http://localhost:8080` → Traefik dashboard

---

## 6️⃣ Domain-based routing (recommended)

Replace the router rules:

```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.app1.rule=Host(`app1.localhost`)"
```

Add to `/etc/hosts`:

```
127.0.0.1 app1.localhost
127.0.0.1 app2.localhost
```

---

## 7️⃣ Optional: Strip path prefix

If your app doesn’t expect `/app1`:

```yaml
labels:
  - "traefik.http.middlewares.app1-strip.stripprefix.prefixes=/app1"
  - "traefik.http.routers.app1.middlewares=app1-strip"
```

---

## 8️⃣ How Traefik routing works (quick mental model)

```
Request
 ↓
EntryPoint (port 80)
 ↓
Router (rule: host/path)
 ↓
Middleware (optional)
 ↓
Service (container + port)
```

---

## 9️⃣ Production upgrades (next steps)

🔒 HTTPS (Let’s Encrypt)

```yaml
--certificatesresolvers.le.acme.httpchallenge=true
--certificatesresolvers.le.acme.httpchallenge.entrypoint=web
--certificatesresolvers.le.acme.acme.email=you@example.com
--certificatesresolvers.le.acme.acme.storage=/letsencrypt/acme.json
```

📈 Load balancing → automatic with replicas
📦 Scaling → `docker-compose up --scale app1=3`

---

## 10️⃣ Common Traefik mistakes

❌ Forgetting `traefik.enable=true`
❌ Wrong internal app port
❌ Using `localhost` inside containers
❌ Exposing app ports unnecessarily

---

If you want, I can:

* Add **HTTPS with Let’s Encrypt**
* Convert this to **Node.js / Flask / Spring Boot**
* Add **authentication middleware**
* Show **Kubernetes (Ingress) equivalent**

Just say the word 🚀

