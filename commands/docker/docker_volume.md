# Docker Volumes — Mini Course

## 1. What Problem Do Volumes Solve?

By default, containers are **ephemeral**:

* When a container is removed → all data inside it is lost

Volumes provide:

* Persistent storage
* Data sharing between containers
* Better performance than bind mounts (in many cases)

---

## 2. Types of Storage in Docker

| Type           | Description       | Use Case               |
| -------------- | ----------------- | ---------------------- |
| **Volume**     | Managed by Docker | Databases, production  |
| **Bind Mount** | Maps host folder  | Dev work, live editing |
| **tmpfs**      | In-memory storage | Sensitive/temp data    |

---

## 3. Basic Volume Commands

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

### Remove volume

```bash
docker volume rm my_volume
```

---

## 4. Using Volumes with `docker run`

### Example: Persist data

```bash
docker run -d \
  --name my_container \
  -v my_volume:/app/data \
  nginx
```

Data inside `/app/data` persists even if container is deleted.

---

## 5. Dockerfile + Volume Example

Let’s build a simple Node.js app that writes logs.

### Project structure

```
project/
 ├── Dockerfile
 └── app.js
```

### app.js

```js
const fs = require('fs');

setInterval(() => {
  fs.appendFileSync('/data/log.txt', `Log at ${new Date()}\n`);
}, 2000);
```

---

### Dockerfile

```Dockerfile
FROM node:18

WORKDIR /app

COPY app.js .

# Create a mount point
VOLUME ["/data"]

CMD ["node", "app.js"]
```

### Important

* `VOLUME` creates an anonymous volume if none is provided
* Best practice: define volumes in **docker-compose**, not Dockerfile

---

## 6. Running the Above Image

```bash
docker build -t log-app .
docker run -d -v my_logs:/data log-app
```

---

## 7. Docker Compose with Volumes (Recommended)

### docker-compose.yml

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: log_app
    volumes:
      - logs_data:/data

volumes:
  logs_data:
```

### Run it

```bash
docker-compose up -d
```

---

## 8. Real-World Example: Database (PostgreSQL)

### docker-compose.yml

```yaml
version: "3.9"

services:
  db:
    image: postgres:15
    container_name: postgres_db
    restart: always
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

Without volume → database resets every restart
With volume → data persists

---

## 9. Bind Mount Example (Dev Mode)

```yaml
services:
  app:
    image: node:18
    working_dir: /app
    volumes:
      - .:/app
    command: node app.js
```

Changes on your local machine reflect instantly inside container

---

## 10. Sharing Volume Between Containers

```yaml
services:
  writer:
    image: busybox
    volumes:
      - shared_data:/data
    command: sh -c "echo Hello > /data/file.txt"

  reader:
    image: busybox
    volumes:
      - shared_data:/data
    command: cat /data/file.txt

volumes:
  shared_data:
```

---

## 11. Best Practices

Use **named volumes** for production
Avoid storing important data inside container filesystem
Use **docker-compose** to manage volumes
Backup volumes regularly
Don’t rely on `VOLUME` in Dockerfile for critical storage

---

## 12. Common Mistakes

Forgetting volume → data loss
Using bind mounts in production incorrectly
Not cleaning unused volumes (`docker volume prune`)

---

## 13. Bonus: Inspect Volume Data

Find volume location:

```bash
docker volume inspect my_volume
```

Then check:

```bash
/var/lib/docker/volumes/
```

---

## 14. Summary

* Containers are temporary → volumes make data permanent
* Use:

  * `docker run -v`
  * `docker-compose volumes`
* Essential for:

  * Databases
  * Logs
  * File storage

---

# Hands-On Docker Volumes Lab

## Exercise 1: Data Loss vs Persistence

### Step 1 — Run WITHOUT a volume

```bash
docker run -it --name temp-container alpine sh
```

Inside container:

```sh
echo "Hello World" > /data.txt
exit
```

Now remove and re-run:

```bash
docker rm temp-container
docker run -it alpine sh
```

Check:

```sh
cat /data.txt
```

File is gone

---

### Step 2 — Run WITH a volume

```bash
docker run -it --name persistent-container -v mydata:/data alpine sh
```

Inside:

```sh
echo "Persistent Data" > /data/file.txt
exit
```

Remove + run again:

```bash
docker rm persistent-container
docker run -it -v mydata:/data alpine sh
```

Check:

```sh
cat /data/file.txt
```

Data is still there

---

## Exercise 2: Inspect Volume Internals

```bash
docker volume inspect mydata
```

Find `"Mountpoint"`

Now on host:

```bash
cd /var/lib/docker/volumes/mydata/_data
ls
```

You’ll see your file

---

## Exercise 3: Dockerfile Volume Behavior

### Create files

**Dockerfile**

```Dockerfile
FROM alpine
RUN mkdir /data
RUN echo "Default Data" > /data/default.txt
VOLUME ["/data"]
CMD ["sh"]
```

---

### Build & Run

```bash
docker build -t volume-test .
docker run -it volume-test
```

Inside:

```sh
ls /data
```

You may NOT see `default.txt` as expected

### Lesson

* Declaring `VOLUME` can override build-time data
* Avoid relying on it for preloaded data

---

## Exercise 4: Named Volume with docker-compose

### docker-compose.yml

```yaml
version: "3.9"

services:
  app:
    image: alpine
    container_name: volume_app
    volumes:
      - mylogs:/logs
    command: sh -c "while true; do date >> /logs/log.txt; sleep 2; done"

volumes:
  mylogs:
```

---

### Run

```bash
docker-compose up -d
```

Check logs:

```bash
docker exec -it volume_app sh
cat /logs/log.txt
```

Stop + restart:

```bash
docker-compose down
docker-compose up -d
```

Logs continue growing (persisted)

---

## Exercise 5: Bind Mount (Live Editing)

Create `app.js`:

```js
setInterval(() => {
  console.log("Hello from container");
}, 2000);
```

Run:

```bash
docker run -it -v $(pwd):/app -w /app node:18 node app.js
```

Edit `app.js` on host → container reflects instantly

---

## Exercise 6: Shared Volume Between Containers

```bash
docker volume create sharedvol
```

### Container 1 (writer)

```bash
docker run -it --name writer -v sharedvol:/data alpine sh
```

Inside:

```sh
echo "Shared Hello" > /data/test.txt
```

---

### Container 2 (reader)

```bash
docker run -it --name reader -v sharedvol:/data alpine sh
```

Inside:

```sh
cat /data/test.txt
```

Same data across containers

---

## Exercise 7: PostgreSQL Persistence

```bash
docker run -d \
  --name pgtest \
  -e POSTGRES_PASSWORD=pass \
  -v pgdata:/var/lib/postgresql/data \
  postgres:15
```

---

### Test it

```bash
docker exec -it pgtest psql -U postgres
```

Inside:

```sql
CREATE DATABASE testdb;
```

---

### Remove & recreate container

```bash
docker rm -f pgtest

docker run -d \
  --name pgtest \
  -e POSTGRES_PASSWORD=pass \
  -v pgdata:/var/lib/postgresql/data \
  postgres:15
```

Database still exists

---

## Exercise 8: Volume Cleanup

List unused volumes:

```bash
docker volume ls
```

Remove unused:

```bash
docker volume prune
```

Be careful—this deletes unused data permanently

---

## Challenge Exercises

### Challenge 1

Create:

* 1 container writes logs
* 1 container reads logs
* Use docker-compose

---

### Challenge 2

Break persistence:

* Run database WITHOUT volume
* Restart container
* Observe data loss

---

### Challenge 3

Mix:

* Bind mount for code
* Volume for database
