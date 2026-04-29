# Docker Persistent Volumes — Mini Course

## 1. Why Persistent Volumes Matter

By default, Docker containers are **ephemeral**:

* When a container is deleted → data is lost
* Not ideal for databases, uploads, logs, etc.

Persistent volumes solve this by storing data **outside the container lifecycle**.

---

## 2. Types of Docker Storage

### 1. Volumes (Recommended)

* Managed by Docker
* Stored in `/var/lib/docker/volumes/`
* Best for production

### 2. Bind Mounts

* Map host directory → container
* Good for development

### 3. tmpfs

* Stored in memory (not persistent)

---

## 3. Key Concepts

| Concept          | Meaning                          |
| ---------------- | -------------------------------- |
| Volume           | Managed storage by Docker        |
| Mount            | Attaching storage to container   |
| Data persistence | Data survives container deletion |

---

# 4. Basic Volume Commands

### Create a volume

```bash
docker volume create my_volume
```

### List volumes

```bash
docker volume ls
```

### Inspect volume

```bash
docker volume inspect my_volume
```

---

# 5. Example 1: Volume with Docker Run

### Run Nginx with a volume

```bash
docker run -d \
  --name nginx_container \
  -v my_volume:/usr/share/nginx/html \
  nginx
```

Now anything inside `/usr/share/nginx/html` is persistent.

---

# 6. Example 2: Bind Mount (Development)

```bash
docker run -d \
  --name dev_container \
  -v $(pwd)/app:/app \
  node:18
```

Your local folder syncs with the container.

---

# 7. Real-World Example: PostgreSQL with Volume

```bash
docker run -d \
  --name postgres_db \
  -e POSTGRES_PASSWORD=secret \
  -v pgdata:/var/lib/postgresql/data \
  postgres
```

Database survives container deletion.

---

# 8. Dockerfile Example (With Volume)

A Dockerfile itself **does NOT persist data**, but you can define a mount point.

### Example: Node.js app

```Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

# Declare volume
VOLUME ["/app/data"]

CMD ["node", "index.js"]
```

This tells Docker:

* `/app/data` should be treated as persistent storage

---

# 9. Docker Compose — Persistent Volumes

## Example 1: Simple Web App

```yaml
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - web_data:/usr/share/nginx/html

volumes:
  web_data:
```

---

## Example 2: Node + MongoDB (Real App)

```yaml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    depends_on:
      - mongo

  mongo:
    image: mongo
    restart: always
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

Key points:

* `mongo_data` persists DB data
* App code is bind-mounted for live reload

---

## Example 3: PostgreSQL + Admin UI

```yaml
version: "3.9"

services:
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - db_data:/var/lib/postgresql/data

  adminer:
    image: adminer
    ports:
      - "8081:8080"

volumes:
  db_data:
```

---

# 10. Named Volume vs Bind Mount

| Feature           | Volume | Bind Mount |
| ----------------- | ------ | ---------- |
| Managed by Docker | ✅      | ❌          |
| Portable          | ✅      | ❌          |
| Easy backup       | ✅      | ⚠️         |
| Dev-friendly      | ❌      | ✅          |

---

# 11. Test Persistence

### Step 1: Run container

```bash
docker run -it -v test_vol:/data ubuntu bash
```

### Step 2: Create file

```bash
echo "hello" > /data/file.txt
exit
```

### Step 3: Delete container

```bash
docker rm <container_id>
```

### Step 4: Run again

```bash
docker run -it -v test_vol:/data ubuntu bash
cat /data/file.txt
```

File still exists ✔️

---

# 12. Cleanup

```bash
docker volume rm my_volume
docker system prune
```

---

# 13. Best Practices

* Use **named volumes** for databases
* Use **bind mounts** for development
* Never store important data inside container only
* Backup volumes regularly

---

# 14. Mini Project (Recommended)

Build:

* Node.js app
* MongoDB database
* Persistent volume for DB

Try:

* Delete container
* Restart
* Verify data still exists

---

# What we Learned

* Why persistence matters
* How Docker volumes work
* How to use volumes in:

  * `docker run`
  * `Dockerfile`
  * `docker-compose`
