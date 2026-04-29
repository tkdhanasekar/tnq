# Docker Networking Course (Beginner → Intermediate)

## Module 1: Networking Basics

### What is Docker Networking?

Docker networking allows containers to:

* Communicate with each other
* Communicate with the host
* Communicate with the outside world

### Default Network Types

Docker provides several network drivers:

1. **bridge (default)** – containers on same host communicate
2. **host** – container shares host network
3. **none** – no networking
4. **overlay** – multi-host networking (Swarm)
5. **macvlan** – assign MAC address to container

---

## Module 2: Bridge Network (Core Concept)

### Create a Custom Network

```bash
docker network create my_bridge_network
```

### Run Containers in Same Network

```bash
docker run -d --name app1 --network my_bridge_network nginx
docker run -d --name app2 --network my_bridge_network busybox sleep 3600
```

### Test Communication

```bash
docker exec -it app2 ping app1
```

Docker provides **automatic DNS resolution** using container names.

---

## Module 3: Dockerfile with Networking Example

We’ll create a simple **Node.js app** that talks to another service.

### App Structure

```
app/
 ├── Dockerfile
 ├── package.json
 └── server.js
```

### server.js

```js
const http = require('http');

const HOST = process.env.TARGET_HOST || 'localhost';

http.createServer((req, res) => {
  res.end(`Hello! Trying to reach: ${HOST}`);
}).listen(3000);
```

---

### Dockerfile

```Dockerfile
FROM node:18

WORKDIR /app

COPY package.json .
RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

---

### Build Image

```bash
docker build -t my-node-app .
```

---

### Run with Network

```bash
docker network create my_net

docker run -d --name service1 --network my_net my-node-app

docker run -d \
  --name service2 \
  --network my_net \
  -e TARGET_HOST=service1 \
  my-node-app
```

`service2` can reach `service1` using container name.

---

## Module 4: Multi-Container Setup with docker-compose

This is where networking becomes powerful.

### Example: Web + Database

---

### docker-compose.yml

```yaml
version: '3.9'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=db
    depends_on:
      - db
    networks:
      - app_network

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    networks:
      - app_network

networks:
  app_network:
    driver: bridge
```

---

### Key Concepts

* `db` is reachable via hostname `db`
* Both services share same network
* No manual linking needed

---

### Run It

```bash
docker-compose up -d
```

---

## Module 5: Advanced Networking Concepts

### Multiple Networks

```yaml
services:
  frontend:
    image: nginx
    networks:
      - front_net

  backend:
    image: node
    networks:
      - back_net

  api:
    image: node
    networks:
      - front_net
      - back_net

networks:
  front_net:
  back_net:
```

`api` acts as a bridge between frontend and backend.

---

### Internal Network (Secure)

```yaml
networks:
  private_net:
    internal: true
```

Prevents external access

---

### Static IP (Advanced)

```yaml
services:
  app:
    image: nginx
    networks:
      my_net:
        ipv4_address: 172.20.0.10

networks:
  my_net:
    ipam:
      config:
        - subnet: 172.20.0.0/16
```

---

## Module 6: Host Networking

```bash
docker run --network host nginx
```

Uses host ports directly (no port mapping needed)

Only recommended for performance-critical apps

---

## Module 7: Debugging Networking

### Inspect Network

```bash
docker network inspect my_net
```

### Check Container IP

```bash
docker inspect container_name
```

### Test Connectivity

```bash
docker exec -it container ping other_container
```

---

## Module 8: Real-World Project Example

### Microservices Setup

```yaml
version: '3.9'

services:
  frontend:
    image: nginx
    ports:
      - "80:80"
    networks:
      - public

  api:
    build: ./api
    networks:
      - public
      - private

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
    networks:
      - private

networks:
  public:
  private:
    internal: true
```

---

## Key Takeaways

* Containers communicate via **DNS names (service names)**
* Use **custom bridge networks** for isolation
* **docker-compose simplifies networking**
* Separate networks = better security
* Avoid hardcoding IPs unless necessary

---

## 🚀 Practice Exercises

1. Create 3 containers:

   * frontend
   * backend
   * database
     → Make backend talk to database

2. Build a compose file where:

   * frontend cannot access database directly

3. Add Redis cache to your network

---

# Docker Networking Hands-On Labs

## Exercise 1: Container-to-Container Communication

### Goal

Make two containers talk using a custom network.

### Steps

```bash
docker network create lab_net
```

```bash
docker run -d --name web --network lab_net nginx
docker run -it --name client --network lab_net busybox sh
```

Inside the `client` container:

```sh
ping web
wget -qO- http://web
```

### Expected Outcome

* `ping` works
* You see HTML from nginx

### What You Learn

* Docker DNS (container name = hostname)

---

## Exercise 2: Build + Connect Your Own App

### Goal

Run two custom apps that communicate.

---

### Create App

**server.js**

```js
const http = require('http');

http.createServer((req, res) => {
  res.end("Hello from Service A");
}).listen(3000);
```

---

### Dockerfile

```Dockerfile
FROM node:18
WORKDIR /app
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

---

### Build & Run

```bash
docker build -t service-a .

docker network create app_net

docker run -d --name service-a --network app_net service-a

docker run -it --network app_net curlimages/curl curl http://service-a:3000
```

### Expected Outcome

Response:

```
Hello from Service A
```

---

## Exercise 3: Multi-Service with docker-compose

### Goal

Connect **web + database**

---

### docker-compose.yml

```yaml
version: '3.9'

services:
  app:
    image: node:18
    working_dir: /app
    volumes:
      - .:/app
    command: node app.js
    environment:
      - DB_HOST=db
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: testdb
```

---

### app.js

```js
console.log("DB Host:", process.env.DB_HOST);
```

---

### Run

```bash
docker-compose up
```

### Expected Outcome

```
DB Host: db
```

### What You Learn

* Service name = hostname
* Compose auto-creates a network

---

## Exercise 4: Network Isolation (Security)

### Goal

Prevent frontend from accessing database directly.

---

### docker-compose.yml

```yaml
version: '3.9'

services:
  frontend:
    image: nginx
    networks:
      - public

  backend:
    image: node:18
    networks:
      - public
      - private

  db:
    image: postgres:15
    networks:
      - private

networks:
  public:
  private:
    internal: true
```

---

### Test

```bash
docker exec -it frontend ping db
```

### Expected

Fails

```bash
docker exec -it backend ping db
```

### Expected

Works

---

## Exercise 5: Load Balancing Simulation

### Goal

Run multiple backend instances and access them via nginx.

---

### docker-compose.yml

```yaml
version: '3.9'

services:
  backend1:
    image: nginx

  backend2:
    image: nginx

  proxy:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
```

---

### nginx.conf

```nginx
events {}

http {
  upstream backend {
    server backend1:80;
    server backend2:80;
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

### Run

```bash
docker-compose up
```

Visit:

```
http://localhost:8080
```

### What You Learn

* Service discovery
* Internal load balancing

---

## Exercise 6: Debugging Network Issues

### Goal

Practice troubleshooting

---

### Commands

```bash
docker network ls
docker network inspect lab_net
```

```bash
docker exec -it container_name sh
```

Inside container:

```sh
ping other_container
nslookup other_container
```

---

### Challenge

Break something intentionally:

* Remove network
* Change container name
* Stop one container

Then debug it.

---

## Exercise 7: Real Microservices Challenge

### Goal

Design this architecture:

```
[Frontend] → [API] → [DB]
                ↓
             [Redis]
```

---

### Requirements

* Frontend:

  * Can access API
  * Cannot access DB

* API:

  * Can access DB + Redis

* DB:

  * Private network only

---

### Hint Structure

```yaml
networks:
  public:
  private:
```

---

## Bonus Challenges

### Challenge 1

Add a **Redis cache** and connect it only to backend

### Challenge 2

Use **environment variables** to switch services dynamically

### Challenge 3

Scale services:

```bash
docker-compose up --scale backend=3
```

---

## What we Should Be Comfortable With After This

* Creating custom networks
* Service-to-service communication
* docker-compose networking
* Network isolation for security
* Debugging connectivity issues
