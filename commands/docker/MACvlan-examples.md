Docker Compose examples using a **macvlan** network. Both assume your LAN is `192.168.1.0/24` and your Docker host's physical interface is `eth0` (replace with your actual interface, e.g., `enp3s0`, `ens18`, etc.).

> **Important:** Containers on a macvlan network typically cannot communicate directly with the Docker host unless you create an additional macvlan interface on the host.

---

# Example 1: Single Nginx Container with Static IP

## Directory Structure

```text
macvlan-nginx/
├── docker-compose.yml
└── nginx.conf
```

## docker-compose.yml

```yaml
version: "3.9"

services:
  nginx:
    image: nginx:latest
    container_name: nginx-macvlan
    restart: unless-stopped

    networks:
      macvlan_net:
        ipv4_address: 192.168.1.100

    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro

networks:
  macvlan_net:
    driver: macvlan
    driver_opts:
      parent: eth0
    ipam:
      config:
        - subnet: 192.168.1.0/24
          gateway: 192.168.1.1
          ip_range: 192.168.1.96/27
```

## nginx.conf

```nginx
server {
    listen 80;

    location / {
        return 200 "Hello from Docker Macvlan!\n";
    }
}
```

## Start

```bash
docker compose up -d
```

## Test

```bash
curl http://192.168.1.100
```

Expected:

```text
Hello from Docker Macvlan!
```

---

# Example 2: Multiple Services (Pi-hole + Nginx) on Macvlan

Useful when services need their own LAN IP addresses.

## Directory Structure

```text
macvlan-services/
├── docker-compose.yml
└── pihole/
    └── etc-pihole/
```

## docker-compose.yml

```yaml
version: "3.9"

services:
  nginx:
    image: nginx:alpine
    container_name: nginx-web

    restart: unless-stopped

    networks:
      lan:
        ipv4_address: 192.168.1.110

  pihole:
    image: pihole/pihole:latest
    container_name: pihole

    hostname: pihole
    restart: unless-stopped

    environment:
      TZ: Asia/Kolkata
      WEBPASSWORD: ChangeMe123

    volumes:
      - ./pihole/etc-pihole:/etc/pihole

    networks:
      lan:
        ipv4_address: 192.168.1.111

networks:
  lan:
    driver: macvlan

    driver_opts:
      parent: eth0

    ipam:
      config:
        - subnet: 192.168.1.0/24
          gateway: 192.168.1.1
          ip_range: 192.168.1.96/27
```

## Start

```bash
docker compose up -d
```

Access:

```text
http://192.168.1.110
http://192.168.1.111/admin
```

---

# Host-to-Container Communication Fix

If the Docker host cannot reach macvlan containers, create a host-side macvlan interface.

## Create Interface

```bash
sudo ip link add macvlan-host link eth0 type macvlan mode bridge

sudo ip addr add 192.168.1.250/32 dev macvlan-host

sudo ip link set macvlan-host up

sudo ip route add 192.168.1.96/27 dev macvlan-host
```

Where:

* `eth0` = physical NIC
* `192.168.1.96/27` = IP range assigned to containers
* `192.168.1.250` = unused IP on your LAN

## Verify

```bash
ping 192.168.1.100
ping 192.168.1.110
```

---

# Finding Your Parent Interface

Linux:

```bash
ip route | grep default
```

Example output:

```text
default via 192.168.1.1 dev ens18
```

Use:

```yaml
driver_opts:
  parent: ens18
```

instead of `eth0`.

---

# Recommended Production Layout

Reserve a dedicated range for Docker macvlan containers:

```text
LAN:          192.168.1.0/24
Gateway:      192.168.1.1
DHCP Range:   192.168.1.10-192.168.1.90
Macvlan Pool: 192.168.1.100-192.168.1.126
```

This avoids IP conflicts between DHCP clients and Docker containers.

