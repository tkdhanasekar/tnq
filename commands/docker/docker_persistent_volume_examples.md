## 1. Create and Use a Named Volume

### Step 1: Create a named volume

```bash
docker volume create my_data
```

### Step 2: Run a container with the volume (detached mode)

```bash
docker run -d \
  --name my_container \
  -v my_data:/app/data \
  nginx
```

### What this does:

* `-d` → runs container in **detached mode** (background)
* `--name my_container` → assigns a name
* `-v my_data:/app/data` → mounts **named volume** `my_data` inside container at `/app/data`

---

## 2. Verify Volume Persistence

### Write data inside container:

```bash
docker exec -it my_container sh -c "echo hello > /app/data/file.txt"
```

### Remove container:

```bash
docker rm -f my_container
```

### Run a new container with same volume:

```bash
docker run -d \
  --name new_container \
  -v my_data:/app/data \
  nginx
```

### Check file:

```bash
docker exec -it new_container cat /app/data/file.txt
```

You’ll still see `hello` → proves **data persists even after container deletion**

---

## 3. Example with MySQL (Real-world use)

```bash
docker volume create mysql_data

docker run -d \
  --name mysql_db \
  -e MYSQL_ROOT_PASSWORD=root123 \
  -v mysql_data:/var/lib/mysql \
  mysql:8
```

### Why this matters:

* MySQL stores data in `/var/lib/mysql`
* Using a named volume ensures your **database survives container restarts/removal**

---

## 4. List and Inspect Volumes

```bash
docker volume ls
docker volume inspect my_data
```

---

## Key Takeaways

* **Named volumes** are managed by Docker and stored outside containers
* Data **persists independently** of container lifecycle
* `-d` flag runs containers in background (detached mode)
* Ideal for databases, logs, uploads, etc.

---

# 1. Simple Docker Compose Example (Nginx + Named Volume)

### `docker-compose.yml`

```yaml
version: "3.9"

services:
  web:
    image: nginx:latest
    container_name: nginx_server
    ports:
      - "8080:80"
    volumes:
      - web_data:/usr/share/nginx/html
    restart: always

volumes:
  web_data:
```

---

## What’s happening here

* `web_data` → **named volume (persistent storage)**
* Mounted to `/usr/share/nginx/html` (Nginx web root)
* Data stored in volume survives container removal
* `restart: always` ensures auto-restart

---

## 2. Run the stack (detached mode)

```bash
docker compose up -d
```

`-d` = runs everything in the background (detached mode)

---

## 3. Test persistence

### Add a file inside the container:

```bash
docker exec -it nginx_server sh -c "echo 'Hello Docker' > /usr/share/nginx/html/index.html"
```

### Open in browser:

```
http://localhost:8080
```

You’ll see:

```
Hello Docker
```

---

## 4. Stop and remove container (BUT keep volume)

```bash
docker compose down
```

This removes containers but **NOT the named volume**

---

## 5. Bring it back (data still exists)

```bash
docker compose up -d
```

Now visit:

```
http://localhost:8080
```

Your `index.html` is still there → volume persisted data

---

# 6. Real-world example: MySQL with named volume

```yaml
version: "3.9"

services:
  db:
    image: mysql:8
    container_name: mysql_db
    environment:
      MYSQL_ROOT_PASSWORD: root123
      MYSQL_DATABASE: appdb
    volumes:
      - mysql_data:/var/lib/mysql
    restart: always

volumes:
  mysql_data:
```

---

## Why this is important

* `/var/lib/mysql` contains all DB files
* Named volume ensures:

  * data survives container deletion
  * safe upgrades / restarts
  * no accidental data loss

---

# Key Takeaways

✔ `volumes:` at bottom defines named volumes
✔ `service: volumes:` mounts them into containers
✔ Data persists even if containers are removed
✔ `docker compose up -d` runs everything in detached mode
