## Run Portainer with Docker

### 1. Create a volume (to persist data)

```bash
docker volume create portainer_data
```

---

### 2. Run Portainer container

```bash
docker run -d \
  -p 8000:8000 \
  -p 9443:9443 \
  --name portainer \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce:latest
```

---

### 3. Access Portainer

Open your browser and go to:

```
https://localhost:9443
```

* First time → create admin user
* Choose **Docker (local)** environment

---

## What this setup does

* `9443` → secure web UI (main dashboard)
* `/var/run/docker.sock` → gives Portainer control over Docker
* `portainer_data` → keeps your settings after restart
* `--restart=always` → auto-start on reboot

---

## Optional: Docker Compose version

If you prefer Compose:

```yaml
version: "3.8"

services:
  portainer:
    image: portainer/portainer-ce:latest
    container_name: portainer
    restart: always
    ports:
      - "8000:8000"
      - "9443:9443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - portainer_data:/data

volumes:
  portainer_data:
```

Run it:

```bash
docker compose up -d
```

---

## Tips

* Use HTTPS (`9443`), not HTTP (`9000`, deprecated)
* For servers: replace `localhost` with your server IP
* Make sure port `9443` is open in firewall
