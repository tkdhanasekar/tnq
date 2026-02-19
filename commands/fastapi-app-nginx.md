**FastAPI website with a hit counter** on **Ubuntu** using **NGINX**

---

## Connect to your server

```bash
ssh root@server
```

Make sure your server has **Python 3.10+** and **pip** installed:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv -y
```

---

## Create your FastAPI app

Create a project folder:

```bash
mkdir ~/fastapi_hit_counter
cd ~/fastapi_hit_counter
python3 -m venv venv
source venv/bin/activate
pip install fastapi uvicorn
```

Create `main.py` with a simple hit counter:

```python
from fastapi import FastAPI
from fastapi.responses import HTMLResponse

app = FastAPI()
hit_count = 0

@app.get("/", response_class=HTMLResponse)
async def root():
    global hit_count
    hit_count += 1
    return f"<h1>Welcome!</h1><p>Hit count: {hit_count}</p>"
```

Test locally:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Visit `http://server_ip:8000` to see the counter in action.

---

## Install & configure Gunicorn (optional but recommended)

For production, we usually use **Uvicorn with Gunicorn**:

```bash
pip install gunicorn
pip install "uvicorn[standard]"
```

Create a systemd service for automatic startup:

```bash
sudo vim /etc/systemd/system/fastapi.service
```

Paste:

```ini
[Unit]
Description=FastAPI Hit Counter
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/root/fastapi_hit_counter
Environment="PATH=/root/fastapi_hit_counter/venv/bin"
ExecStart=/root/fastapi_hit_counter/venv/bin/uvicorn main:app --host 0.0.0.0 --port 8000

[Install]
WantedBy=multi-user.target
```

Enable & start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable fastapi
sudo systemctl start fastapi
sudo systemctl status fastapi
```

---

## Install NGINX

```bash
sudo apt install nginx -y
```

Create a site config:

```bash
sudo vim /etc/nginx/sites-available/fastapi
```

Paste:

```nginx
server {
    listen 80;
    server_name server_ip;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable the site and restart NGINX:

```bash
sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl restart nginx
```

FastAPI app should be reachable at:

```
http://server_ip
```
