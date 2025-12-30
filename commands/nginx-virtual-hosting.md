**step-by-step instructions** to configure **two virtual hosts (server blocks)** in **NGINX on Ubuntu** for:

* `apple.hashlabs.in`
* `orange.hashlabs.in`

### Install NGINX (if not installed)

```bash
sudo apt update
sudo apt install nginx -y
```

---

## Create Web Root Directories

Create separate folders for each site.

```bash
sudo mkdir -p /var/www/apple.hashlabs.in
sudo mkdir -p /var/www/orange.hashlabs.in
```

Set ownership and permissions:

```bash
sudo chown -R $USER:$USER /var/www/apple.hashlabs.in
sudo chown -R $USER:$USER /var/www/orange.hashlabs.in
sudo chmod -R 755 /var/www
```

---

## Create Sample Index Files

This helps verify each site works.

### Apple site

```bash
vim /var/www/apple.hashlabs.in/index.html
```

```html
<h1>Apple Site</h1>
<p>apple.hashlabs.in is working!</p>
```

### Orange site

```bash
vim /var/www/orange.hashlabs.in/index.html
```

```html
<h1>Orange Site</h1>
<p>orange.hashlabs.in is working!</p>
```

---

## Create NGINX Server Block Files

### Apple virtual host

```
sudo vim /etc/nginx/sites-available/apple.hashlabs.in
```

```nginx
server {
    listen 80;
    server_name apple.hashlabs.in www.apple.hashlabs.in;

    root /var/www/apple.hashlabs.in;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

### Orange virtual host

```
sudo vim /etc/nginx/sites-available/orange.hashlabs.in
```

```nginx
server {
    listen 80;
    server_name orange.hashlabs.in www.orange.hashlabs.in;

    root /var/www/orange.hashlabs.in;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

## Enable the Virtual Hosts

Create symbolic links to `sites-enabled`:

```
sudo ln -s /etc/nginx/sites-available/apple.hashlabs.in /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/orange.hashlabs.in /etc/nginx/sites-enabled/
```

(Optional) Disable default site:

```bash
sudo unlink /etc/nginx/sites-enabled/default
```

---

## Test NGINX Configuration

```bash
sudo nginx -t
```

---

## Reload NGINX

```bash
sudo systemctl reload nginx
```

---

## Enable HTTPS with Let’s Encrypt

```bash
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx
```
