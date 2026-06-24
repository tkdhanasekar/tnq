To set up a simple **Docker Swarm** on Ubuntu and run **3 replicas of NGINX**, follow these steps.

## 1. Install Docker

Update packages and install Docker:

```bash
sudo apt update
sudo apt install -y docker.io
```

Enable and start Docker:

```bash
sudo systemctl enable docker
sudo systemctl start docker
```

Verify:

```bash
docker --version
docker info
```

---

## 2. Initialize Docker Swarm

On the manager node:

```bash
docker swarm init
```

Example output:

```text
Swarm initialized: current node (abc123) is now a manager.

To add a worker to this swarm, run:

docker swarm join --token SWMTKN-1-xxxxx 192.168.1.10:2377
```

If using multiple servers, run the displayed `docker swarm join` command on each worker node.

Check swarm status:

```bash
docker node ls
```

---

## 3. Create an NGINX Service with 3 Replicas

```bash
docker service create \
  --name nginx-web \
  --replicas 3 \
  -p 80:80 \
  nginx:latest
```

This will:

* Pull the NGINX image
* Create a service named `nginx-web`
* Run 3 replicas
* Publish port 80

---

## 4. Verify the Service

List services:

```bash
docker service ls
```

Expected output:

```text
ID            NAME        MODE        REPLICAS   IMAGE
abc123        nginx-web   replicated  3/3        nginx:latest
```

View tasks (containers):

```bash
docker service ps nginx-web
```

---

## 5. Test NGINX

From the manager node:

```bash
curl http://localhost
```

Or from another machine:

```bash
curl http://<manager-ip>
```

You should see the default NGINX welcome page HTML.

---

## 6. Scale the Service

Increase replicas to 5:

```bash
docker service scale nginx-web=5
```

Check:

```bash
docker service ls
```

---

## 7. Update the Service

For example, switch to a specific NGINX version:

```bash
docker service update \
  --image nginx:1.27 \
  nginx-web
```

---

## 8. Remove the Service

```bash
docker service rm nginx-web
```

---

## 9. Leave the Swarm (Optional)

Worker node:

```bash
docker swarm leave
```

Manager node:

```bash
docker swarm leave --force
```

### Quick Demo Commands

```bash
sudo apt update
sudo apt install -y docker.io

sudo systemctl enable --now docker

docker swarm init

docker service create \
  --name nginx-web \
  --replicas 3 \
  -p 80:80 \
  nginx:latest

docker service ls
docker service ps nginx-web
```

This gives you a working Docker Swarm cluster (single-manager or multi-node) with **3 NGINX replicas managed by Swarm**.

