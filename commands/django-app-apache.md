**Django application with Apache on Ubuntu** using **mod_wsgi**

---

# 1. Install Required Packages

Update your system first:

```bash
sudo apt update
```

Install Apache, Python tools, and mod_wsgi:

```bash
sudo apt install apache2 python3-pip python3-venv libapache2-mod-wsgi-py3
```

Enable mod_wsgi:

```bash
sudo a2enmod wsgi
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

---

# 2. Create Your Django Project

Go to your desired directory:

```bash
mkdir /var/www/myproject
cd /var/www/myproject
```

Create virtual environment:

```bash
python3 -m venv venv
source venv/bin/activate
```

Install Django:

```bash
pip install django
```

Create project:

```bash
django-admin startproject myproject .
```

Test it:

```bash
python manage.py runserver 0.0.0.0:8000
```

Stop the server after testing.

---

# 3. Configure Django for Production

Edit:

```bash
vim myproject/settings.py
```

### Important changes:

### Set Allowed Hosts

```python
ALLOWED_HOSTS = ['your_server_ip', 'your_domain']
```

### Configure Static Files

```python
STATIC_ROOT = BASE_DIR / 'static'
```
save and exit

Then collect static files:

```bash
python manage.py collectstatic
```

---

# 4. Configure Apache

Create a new Apache config file:

```bash
sudo vim /etc/apache2/sites-available/myproject.conf
```

Add this configuration:

```apache
<VirtualHost *:80>
    ServerName your_domain/server_ip
    ServerAdmin admin@example.com

    Alias /static /var/www/myproject/static
    <Directory /var/www/myproject/static>
        Require all granted
    </Directory>

    <Directory /var/www/myproject/myproject>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>

    WSGIDaemonProcess myproject python-path=/var/www/myproject python-home=/var/www/myproject/venv
    WSGIProcessGroup myproject
    WSGIScriptAlias / /var/www/myproject/myproject/wsgi.py

    ErrorLog ${APACHE_LOG_DIR}/myproject_error.log
    CustomLog ${APACHE_LOG_DIR}/myproject_access.log combined
</VirtualHost>
```

---

# 5. Enable the Site

Disable default site (optional but recommended):

```bash
sudo a2dissite 000-default.conf
```

Enable your project:

```bash
sudo a2ensite myproject.conf
```

Test Apache config:

```bash
sudo apache2ctl configtest
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

---

# 6. Set Permissions

Give Apache access:

```bash
sudo chown -R www-data:www-data /var/www/myproject
sudo chmod -R 755 /var/www/myproject
```

---

# 8. Access Your Site

Open in browser:

```
http://your_server_ip
```

or

```
http://your_domain
```

---

# Enable HTTPS with Let’s Encrypt

Install Certbot:

```bash
sudo apt install certbot python3-certbot-apache
```

Run:

```bash
sudo certbot --apache
```

Follow the prompts.

---

# Final Project Structure

```
/var/www/myproject/
 ├── venv/
 ├── myproject/
 │    ├── settings.py
 │    ├── wsgi.py
 ├── static/
 ├── manage.py
```

---

Django app is now running with:

* Apache
* mod_wsgi
* Virtual environment
* Static files configured
* Optional SSL

To login Django admin page
create user and password
```
python manage.py migrate
```
```
python manage.py createsuperuser
```
login
```
http://server_ip/admin
```
