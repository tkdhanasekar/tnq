**FastAPI hit counter app** running on **Apache** on **Ubuntu**
---

## Install Required Packages

Update Ubuntu and install dependencies:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv apache2 libapache2-mod-proxy-uwsgi -y
```

(Optional: `libapache2-mod-proxy-uwsgi` for uWSGI proxying)

---

## Create FastAPI App with Hit Counter

Create a project folder:

```bash
mkdir ~/fastapi_hit_counter
cd ~/fastapi_hit_counter
python3 -m venv venv
source venv/bin/activate
pip install fastapi uvicorn
```

Create `app.py`:

```python
from fastapi import FastAPI
from fastapi.responses import JSONResponse
import threading

app = FastAPI()
lock = threading.Lock()
hits = 0

@app.get("/")
def read_root():
    global hits
    with lock:
        hits += 1
        count = hits
    return JSONResponse(content={"message": f"Hello! This page has been visited {count} times."})
```

This simple version uses **thread-safe in-memory counter**.

---

## Test Locally

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

Visit `http://your_server_ip:8000/` and the hit counter should increment.

---

## Configure Apache as a Reverse Proxy

Apache will forward requests to FastAPI running via Uvicorn. Enable necessary modules:

```bash
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo systemctl restart apache2
```

Create a new site file:

```bash
sudo vim /etc/apache2/sites-available/fastapi_hit_counter.conf
```

Add:

```apache
<VirtualHost *:80>
    ServerName yourdomain.com
    ServerAdmin admin@yourdomain.com

    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/

    ErrorLog ${APACHE_LOG_DIR}/fastapi_error.log
    CustomLog ${APACHE_LOG_DIR}/fastapi_access.log combined
</VirtualHost>
```

Enable the site and reload Apache:

```bash
sudo a2ensite fastapi_hit_counter.conf
sudo systemctl reload apache2
```

---

## Run FastAPI in the Background

Use **systemd** to run FastAPI automatically on boot.

Create service file:

```bash
sudo vim /etc/systemd/system/fastapi.service
```

Add:

```ini
[Unit]
Description=FastAPI Hit Counter App
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/root/fastapi_hit_counter
Environment="PATH=/root/fastapi_hit_counter/venv/bin"
ExecStart=/root/fastapi_hit_counter/venv/bin/uvicorn app:app --host 127.0.0.1 --port 8000

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable fastapi
sudo systemctl start fastapi
sudo systemctl status fastapi
```

Now Apache proxies requests to FastAPI running in the background.

check with 
http://server_ip

