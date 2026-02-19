**FastAPI hit counter app**

> FastAPI (Uvicorn) → Reverse Proxy → Apache → Public IP

Apache will forward requests to Uvicorn running your FastAPI app.


## Install Required Packages

SSH into your server:

```bash
ssh root@server_ip
```

Update system:

```bash
apt update
```

Install dependencies:

```bash
apt install python3-pip python3-venv apache2 -y
```

Enable Apache proxy modules:

```bash
a2enmod proxy
a2enmod proxy_http
a2enmod headers
systemctl restart apache2
```

---

## Setup Python Virtual Environment

```bash
mkdir fastapi-demo
cd /root/fastapi-demo
python3 -m venv venv
source venv/bin/activate
```

Install FastAPI + Uvicorn:

```bash
pip install fastapi uvicorn
```

If your hit counter uses SQLite:

```bash
pip install sqlalchemy
```

---

## Test Your FastAPI App

Make sure your app file looks like this:

`main.py`

```python
from fastapi import FastAPI

app = FastAPI()

counter = 0

@app.get("/")
def home():
    global counter
    counter += 1
    return {"hits": counter}
```

Run it manually:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

Test in browser:

```
http://server_ip:8000
```

If it works → press `CTRL+C`

---

## Create Systemd Service

Create service file:

```bash
vim /etc/systemd/system/fastapi.service
```

Paste:

```ini
[Unit]
Description=FastAPI App
After=network.target

[Service]
User=root
WorkingDirectory=/root/fastapi-demo
ExecStart=/root/fastapi-demo/venv/bin/uvicorn main:app --host 127.0.0.1 --port 8000
Restart=always

[Install]
WantedBy=multi-user.target
```

Save and run:

```bash
systemctl daemon-reload
systemctl start fastapi
systemctl enable fastapi
systemctl status fastapi
```

Your app now runs internally on:

```
http://127.0.0.1:8000
```

---

## Configure Apache Reverse Proxy

Create new Apache config:

```bash
vim /etc/apache2/sites-available/fastapi.conf
```

Paste:

```apache
<VirtualHost *:80>
    ServerName server_ip

    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/

    ErrorLog ${APACHE_LOG_DIR}/fastapi_error.log
    CustomLog ${APACHE_LOG_DIR}/fastapi_access.log combined
</VirtualHost>
```

Enable site:

```bash
a2ensite fastapi.conf
a2dissite 000-default.conf
systemctl reload apache2
```

Now visit:

```
http://server_ip
```

Apache → forwards → Uvicorn → FastAPI → Hit Counter Works
