Docker Compose examples that use **`network_mode: "none"`**, which disables all networking inside the container.

---

# Example 1: Alpine Container with No Network

### Directory Structure

```text
example1/
├── docker-compose.yml
└── hello.sh
```

### docker-compose.yml

```yaml
version: "3.9"

services:
  alpine-test:
    image: alpine:latest
    container_name: alpine-test
    network_mode: "none"
    volumes:
      - ./hello.sh:/hello.sh:ro
    command: sh /hello.sh
```

### hello.sh

```sh
#!/bin/sh

echo "Container started"
echo "Network interfaces:"
ip addr

echo "Trying to ping Google..."
ping -c 1 8.8.8.8 || echo "Network unavailable"

sleep 300
```

### Run

```bash
chmod +x hello.sh
docker compose up
```

### Verify

Inside the container:

```bash
docker exec -it alpine-test sh
```

Check networking:

```bash
ip addr
```

You should only see the loopback interface (`lo`).

---

# Example 2: Python Application with No Network

### Directory Structure

```text
example2/
├── docker-compose.yml
├── Dockerfile
└── app.py
```

### docker-compose.yml

```yaml
version: "3.9"

services:
  python-app:
    build: .
    container_name: python-app
    network_mode: "none"
    restart: unless-stopped
```

### Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY app.py .

CMD ["python", "app.py"]
```

### app.py

```python
import socket
import time

print("Container started")

try:
    socket.gethostbyname("google.com")
    print("DNS resolution succeeded")
except Exception as e:
    print(f"DNS resolution failed: {e}")

while True:
    print("Running without network...")
    time.sleep(30)
```

### Build and Run

```bash
docker compose up --build
```

### Verify

```bash
docker exec -it python-app sh
```

Check interfaces:

```bash
ip addr
```

Expected output:

```text
1: lo: <LOOPBACK,UP,LOWER_UP> ...
```

No `eth0` interface will exist because `network_mode: "none"` completely disables container networking.

---

### Notes

When using:

```yaml
network_mode: "none"
```

you **cannot** use:

```yaml
ports:
networks:
links:
extra_hosts:
dns:
```

because the container is detached from all Docker networks and only has the loopback (`lo`) interface available.

