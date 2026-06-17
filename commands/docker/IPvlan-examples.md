Docker Compose examples using an **IPvlan L2 network**. Both assume your host NIC is `eth0` (change it to match your system, e.g., `ens18`, `enp3s0`, etc.).

---

# Example 1: Two Containers on the Same LAN

### Network Layout

* Physical network: `192.168.1.0/24`
* Gateway: `192.168.1.1`
* Host NIC: `eth0`
* Container IPs:

  * nginx: `192.168.1.100`
  * alpine: `192.168.1.101`

## docker-compose.yml

```yaml
version: "3.9"

services:
  nginx:
    image: nginx:latest
    container_name: ipvlan-nginx
    networks:
      ipvlan_net:
        ipv4_address: 192.168.1.100

  alpine:
    image: alpine:latest
    container_name: ipvlan-alpine
    command: sleep infinity
    networks:
      ipvlan_net:
        ipv4_address: 192.168.1.101

networks:
  ipvlan_net:
    driver: ipvlan
    driver_opts:
      parent: eth0
      ipvlan_mode: l2
    ipam:
      config:
        - subnet: 192.168.1.0/24
          gateway: 192.168.1.1
```

## Deploy

```bash
docker compose up -d
```

## Verify

```bash
docker inspect ipvlan-nginx
```

```bash
docker exec -it ipvlan-alpine ping 192.168.1.100
```

---

# Example 2: Host ↔ Container Communication with IPvlan

A common IPvlan limitation is that the host cannot directly communicate with containers on the same IPvlan network. To fix that, create an IPvlan interface on the host.

### Network Layout

| Device                | IP            |
| --------------------- | ------------- |
| Host IPvlan Interface | 192.168.50.10 |
| Container App1        | 192.168.50.20 |
| Container App2        | 192.168.50.21 |
| Gateway               | 192.168.50.1  |

---

## docker-compose.yml

```yaml
version: "3.9"

services:
  app1:
    image: nginx:latest
    container_name: app1
    networks:
      ipvlan50:
        ipv4_address: 192.168.50.20

  app2:
    image: httpd:latest
    container_name: app2
    networks:
      ipvlan50:
        ipv4_address: 192.168.50.21

networks:
  ipvlan50:
    driver: ipvlan
    driver_opts:
      parent: eth0
      ipvlan_mode: l2
    ipam:
      config:
        - subnet: 192.168.50.0/24
          gateway: 192.168.50.1
```

---

## Host Configuration

Create an IPvlan interface on the host:

### create-ipvlan-host.sh

```bash
#!/bin/bash

ip link add ipvlan0 link eth0 type ipvlan mode l2

ip addr add 192.168.50.10/24 dev ipvlan0

ip link set ipvlan0 up
```

Make executable:

```bash
chmod +x create-ipvlan-host.sh
```

Run:

```bash
sudo ./create-ipvlan-host.sh
```

---

## Optional Cleanup Script

### remove-ipvlan-host.sh

```bash
#!/bin/bash

ip link delete ipvlan0
```

---

## Start Stack

```bash
docker compose up -d
```

---

## Test Connectivity

From host:

```bash
ping 192.168.50.20
```

```bash
curl http://192.168.50.20
```

```bash
curl http://192.168.50.21
```

---

# Alternative: Create Network First, Then Use Compose

Some teams prefer managing IPvlan networks separately.

### create-network.sh

```bash
docker network create -d ipvlan \
  --subnet=192.168.60.0/24 \
  --gateway=192.168.60.1 \
  -o parent=eth0 \
  -o ipvlan_mode=l2 \
  ipvlan60
```

### docker-compose.yml

```yaml
version: "3.9"

services:
  web:
    image: nginx
    networks:
      ipvlan60:
        ipv4_address: 192.168.60.10

networks:
  ipvlan60:
    external: true
```

Deploy:

```bash
./create-network.sh
docker compose up -d
```

Before using any example, verify your NIC name:

```bash
ip link show
```

and replace `eth0` everywhere with the correct interface name.

