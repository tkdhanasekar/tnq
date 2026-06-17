Docker networking commands 

# 1. List Networks

```bash
docker network ls
```

Example output:

```text
NETWORK ID     NAME      DRIVER    SCOPE
a1b2c3d4e5f6   bridge    bridge    local
b2c3d4e5f6g7   host      host      local
c3d4e5f6g7h8   none      null      local
```

---

# 2. Create a Network

## Create a bridge network

```bash
docker network create my-network
```

Or explicitly:

```bash
docker network create --driver bridge my-network
```

### Verify

```bash
docker network ls
```

---

## Create a subnet-specific network

```bash
docker network create \
  --driver bridge \
  --subnet 172.20.0.0/16 \
  --gateway 172.20.0.1 \
  custom-net
```

---

# 3. Inspect a Network

Shows detailed network configuration.

```bash
docker network inspect my-network
```

Example:

```bash
docker network inspect bridge
```

---

# 4. Remove a Network

```bash
docker network rm my-network
```

Remove multiple:

```bash
docker network rm net1 net2 net3
```

---

# 5. Prune Unused Networks

Deletes networks not used by any container.

```bash
docker network prune
```

Force without confirmation:

```bash
docker network prune -f
```

---

# 6. Connect a Container to a Network

Create container:

```bash
docker run -d --name web nginx
```

Connect:

```bash
docker network connect my-network web
```

Verify:

```bash
docker inspect web
```

---

## Connect with Static IP

```bash
docker network connect \
  --ip 172.20.0.10 \
  custom-net web
```

---

# 7. Disconnect a Container from a Network

```bash
docker network disconnect my-network web
```

Force disconnect:

```bash
docker network disconnect -f my-network web
```

---

# 8. Run a Container in a Specific Network

```bash
docker run -d \
  --name app \
  --network my-network \
  nginx
```

---

## Assign Static IP During Creation

```bash
docker run -d \
  --name app \
  --network custom-net \
  --ip 172.20.0.5 \
  nginx
```

---

# 9. Display Container Network Information

```bash
docker inspect container_name
```

Filter network section:

```bash
docker inspect \
  -f '{{json .NetworkSettings.Networks}}' \
  container_name
```

Example:

```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' web
```

Output:

```text
172.20.0.5
```

---

# 10. View Docker Network Details Using Formatting

```bash
docker network inspect bridge \
  --format '{{json .IPAM.Config}}'
```

---

# 11. Check Network Driver

```bash
docker network inspect my-network \
  --format '{{.Driver}}'
```

Output:

```text
bridge
```

---

# 12. Create Different Network Types

## Bridge Network

```bash
docker network create --driver bridge bridge-net
```

---

## Host Network (Linux)

```bash
docker run --network host nginx
```

Container shares host networking stack.

---

## None Network

```bash
docker run --network none nginx
```

Container gets no network interface except loopback.

---

## Overlay Network (Docker Swarm)

Create swarm:

```bash
docker swarm init
```

Create overlay network:

```bash
docker network create \
  --driver overlay \
  my-overlay
```

---

## Macvlan Network

```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 \
  macvlan-net
```

---

# 13. Network Aliases

Create container with alias:

```bash
docker run -d \
  --name db \
  --network my-network \
  --network-alias mysql \
  mysql
```

Other containers can resolve:

```bash
ping mysql
```

---

# 14. Container DNS Settings

Custom DNS:

```bash
docker run -d \
  --dns 8.8.8.8 \
  nginx
```

Multiple DNS servers:

```bash
docker run -d \
  --dns 8.8.8.8 \
  --dns 1.1.1.1 \
  nginx
```

---

# 15. Publish Ports

Map host port to container port:

```bash
docker run -d \
  -p 8080:80 \
  nginx
```

Access:

```text
http://localhost:8080
```

---

Map specific IP:

```bash
docker run -d \
  -p 127.0.0.1:8080:80 \
  nginx
```

---

Map UDP port:

```bash
docker run -d \
  -p 53:53/udp \
  dns-container
```

---

# 16. View Port Mappings

```bash
docker port container_name
```

Example:

```bash
docker port nginx
```

Output:

```text
80/tcp -> 0.0.0.0:8080
```

---

# 17. Network Statistics

View interface statistics from inside container:

```bash
docker exec container_name ip addr
```

Or:

```bash
docker exec container_name ifconfig
```

---

# 18. Test Connectivity Between Containers

Create network:

```bash
docker network create test-net
```

Run containers:

```bash
docker run -dit --name c1 --network test-net alpine
docker run -dit --name c2 --network test-net alpine
```

Test:

```bash
docker exec c1 ping c2
```

---

# 19. Docker Compose Networking

Default network:

```yaml
services:
  app:
    image: nginx

  db:
    image: mysql
```

Start:

```bash
docker compose up -d
```

Containers communicate using service names:

```bash
ping db
```

---

Custom network:

```yaml
services:
  app:
    image: nginx
    networks:
      - backend

  db:
    image: mysql
    networks:
      - backend

networks:
  backend:
    driver: bridge
```

---

# 20. Useful Troubleshooting Commands

View container IP:

```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name
```

Check routes:

```bash
docker exec container_name ip route
```

Check DNS resolution:

```bash
docker exec container_name nslookup google.com
```

Check listening ports:

```bash
docker exec container_name netstat -tulpn
```

Or:

```bash
docker exec container_name ss -tulpn
```

---

# Quick Reference

| Command                     | Purpose                    |
| --------------------------- | -------------------------- |
| `docker network ls`         | List networks              |
| `docker network create`     | Create network             |
| `docker network inspect`    | Show network details       |
| `docker network connect`    | Attach container           |
| `docker network disconnect` | Detach container           |
| `docker network rm`         | Remove network             |
| `docker network prune`      | Delete unused networks     |
| `docker run --network`      | Start container on network |
| `docker port`               | Show port mappings         |
| `docker inspect`            | View IP/network settings   |
| `docker run -p`             | Publish ports              |
| `docker exec ... ping`      | Test connectivity          |

For day-to-day Docker work, the commands you'll use most often are:

```bash
docker network ls
docker network create my-net
docker run --network my-net ...
docker network inspect my-net
docker network connect my-net container
docker network disconnect my-net container
docker network rm my-net
```

1. Create a Docker Network
```
docker network create my-network
```
2. List Docker Networks
```
docker network ls
```
3. Inspect a Docker Network
```
docker network inspect my-network
```
Provides detailed information about the my-network, such as connected containers, subnet, and configuration.
4. Remove a Docker Network
```
docker network rm my-network
```
5. Remove all networks with a single command
```
docker network prune
```

Creating a Docker Network
To create a new network, use the docker network create command. You can specify the driver (like bridge or host) with the -d flag. If you don't include this flag, Docker will create a bridge network by default.
```
docker network create demo-network -d bridge
```
Connecting Containers to Networks
```
docker run -it --rm --name container1 --network demo-network busybox:latest
```
```
docker run -it --rm --name container2 busybox:latest
```
try to communicate between the two containers using their names
```
in container1
/ # ping container2
ping: bad address 'container2'
```
To connect container2 to the network
```
docker network connect demo-network container2
```
```
communicate:
in container1
/ # ping container2
PING container2 (172.22.0.3): 56 data bytes
64 bytes from 172.22.0.3: seq=0 ttl=64 time=4.205 ms
```

## Using Host Networking
While bridge networks are commonly used to connect containers, you can also use host networking, which connects containers directly to the host's network interfaces. To enable host networking, run:
```
docker run -d --name nginx --network host nginx:latest
```
With this setup, NGINX listens on port 80 by default, and you can access it via localhost:80 on your host:
```
curl localhost:80
```
You should see the NGINX welcome page.

## Disabling Networking
To completely disable a container's network connectivity, you can attach it to the none network:
```
docker run -it --rm --network none busybox:latest
```
```
/ # ping google.com
ping: bad address 'google.com'
```
This isolates the container, allowing you to sandbox unknown services.


## Removing Containers from Networks
Docker allows you to manage network connections without needing to restart your containers. You can remove a container from a network like this:
```
docker network disconnect demo-network container2
```
Any changes you make will apply immediately.
