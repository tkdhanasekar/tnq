Here’s a **production-style Docker Compose setup** that combines:

* named volumes (persistent storage)
* custom networks (service isolation)
* secrets (secure credentials)
* environment files (.env)
* multi-service architecture (app + DB + reverse proxy pattern)

---

# Production-Ready Docker Compose Example

## Project structure

```
project/
│── docker-compose.yml
│── .env
│── secrets/
│     └── db_password.txt
```

---

#  1. `.env` file (environment variables)

```env
APP_PORT=8080
MYSQL_DATABASE=appdb
MYSQL_USER=appuser
```

Never hardcode sensitive values here (only config-level data)

---

#  2. Secret file (secure password storage)

```bash id="sec1"
echo "super_strong_password_123" > secrets/db_password.txt
```

---

#  3. Production `docker-compose.yml`

```yaml id="prod1"
version: "3.9"

services:

  app:
    image: nginx:alpine
    container_name: web_app
    ports:
      - "${APP_PORT}:80"
    volumes:
      - app_data:/usr/share/nginx/html
    networks:
      - frontend
    restart: always

  db:
    image: mysql:8.0
    container_name: mysql_db
    environment:
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD_FILE: /run/secrets/db_password
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_password
    secrets:
      - db_password
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - backend
    restart: always

  adminer:
    image: adminer
    container_name: db_admin
    ports:
      - "8081:8080"
    networks:
      - backend
    restart: always

#  Named Volumes (persistent storage)
volumes:
  app_data:
  db_data:

#  Networks (service isolation)
networks:
  frontend:
  backend:

#  Secrets (secure password handling)
secrets:
  db_password:
    file: ./secrets/db_password.txt
```

---

# What makes this production-ready?

## 1. Secrets (NOT environment variables)

* Password stored in file
* Injected securely into container
* Avoids exposure in logs or `docker inspect`

Used via:

```yaml
secrets:
  - db_password
```

---

## 2. Networks (segmentation)

| Network  | Purpose                            |
| -------- | ---------------------------------- |
| frontend | public-facing services (nginx/app) |
| backend  | internal DB communication          |

DB is NOT exposed to frontend directly

---

## 3. Named Volumes (data safety)

```yaml
db_data:/var/lib/mysql
```

* Survives container restart/removal
* Critical for databases

---

## 4. Environment file (.env)

Used for:

```yaml
${APP_PORT}
${MYSQL_DATABASE}
${MYSQL_USER}
```

Keeps config separate from code

---

# Run in production mode (detached)

```bash id="run1"
docker compose --env-file .env up -d
```

---

# Verify setup

### Containers running

```bash id="check1"
docker ps
```

### Networks

```bash id="check2"
docker network ls
```

### Volumes

```bash id="check3"
docker volume ls
```

---

# Architecture summary

```
[ Browser ]
     |
     v
  app (nginx)  ---> frontend network
     |
     v
  db (mysql)   ---> backend network (isolated)
     |
     v
 persistent storage (db_data volume)

Secrets injected securely (not visible in env vars)
```

---

# Key production best practices shown here

✔ Separate frontend/backend networks
✔ Never expose DB to public network
✔ Use `.env` for configuration
✔ Use Docker secrets for passwords
✔ Use named volumes for persistence
✔ Run services in detached mode
✔ Use restart policies for resilience

