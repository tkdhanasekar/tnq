deploy a Flask application using Apache on Ubuntu** with **mod_wsgi**

---

# 1. Update Your Ubuntu Server

```bash
sudo apt update
```

---

# 2. Install Required Packages

Install Apache, Python, pip, virtualenv, and mod_wsgi:

```bash
sudo apt install apache2 python3 python3-pip python3-venv libapache2-mod-wsgi-py3 -y
```

Enable Apache and start it:

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

---

# 3. Create Project Directory

Example project structure:

```bash
sudo mkdir -p /var/www/myflaskapp
sudo chown -R $USER:$USER /var/www/myflaskapp
cd /var/www/myflaskapp
```

---

# 4. Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

Install Flask (and other dependencies):

```bash
pip install flask
```

---

# 5. Create Flask Application

Create `app.py`:

```python
from flask import Flask

app = Flask(__name__)

counter = 0

@app.route("/")
def home():
    global counter
    counter += 1
    return f"Page visited {counter} times"

if __name__ == "__main__":
    app.run()
```

Test locally:

```bash
python app.py
```
Press CTRL+C to stop.

---

# 6. Create WSGI File

Create `myflaskapp.wsgi`:

```python
import sys
sys.path.insert(0, "/var/www/myflaskapp")

from app import app as application
```

---

# 7. Configure Apache

Create a new config file:

```bash
sudo vim /etc/apache2/sites-available/myflaskapp.conf
```

Add:

```apache
<VirtualHost *:80>
    ServerName your_domain_or_ip

    
    WSGIProcessGroup myflaskapp
    WSGIScriptAlias / /var/www/myflaskapp/myflaskapp.wsgi

    <Directory /var/www/myflaskapp>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/myflaskapp_error.log
    CustomLog ${APACHE_LOG_DIR}/myflaskapp_access.log combined
</VirtualHost>
WSGIDaemonProcess myflaskapp python-home=/var/www/myflaskapp/venv python-path=/var/www/myflaskapp

```

---

# 8. Enable Site & Restart Apache

```bash
sudo a2ensite myflaskapp.conf
sudo a2enmod wsgi
sudo systemctl restart apache2
```

---

# 9. Test Your App

Open browser:

```
http://your_server_ip
```

You should see:

```
Page visited times
```

---

# Enable HTTPS with Let’s Encrypt

Install Certbot:

```bash
sudo apt install certbot python3-certbot-apache -y
```

Run:

```bash
sudo certbot --apache
```

---

# Recommended Production Structure

```
/var/www/myflaskapp/
    ├── venv/
    ├── app.py
    ├── myflaskapp.wsgi
```

---

### 500 Internal Server Error

Check logs:

```bash
sudo tail -f /var/log/apache2/error.log
```

### Permission Errors

```bash
sudo chown -R www-data:www-data /var/www/myflaskapp
```
