update the server
```
apt update
```
install nginx
```
apt install nginx -y
```
start, enable, check status
```
systemctl start nginx && systemctl enable nginx && systemctl status nginx --no-pager
```
change the default document root
```
cd /var/www/html
```
```
rm index.html
```
create custom index.html file
```
vim index.html
```
```
<h1>Nginx Webserver Test Page</h1>
```
save and exit
restart the apache service
```
systemctl restart nginx
```
Test nginx configuration files for syntax errors using
```
nginx -t
```
check in browser
http://url

**LetsEncrypt SSL certificate for nginx webserver**
install packages
```
apt install certbot python3-certbot-nginx
```
```
certbot --nginx
```
or
```
certbot --nginx -d yourdomain.com
```
To check for the certificates
```
certbot certificates
```
To renew certbot certification, Test renewal safely (recommended)
```
certbot renew --dry-run
```
then
```
certbot renew
```
To Revoke the SSL certificate using the certificate path
```
certbot revoke --cert-path /etc/letsencrypt/live/yourdomain.com/cert.pem
```
Certbot will ask for confirmation.
or
Revoke by domain name
```
certbot revoke --cert-name yourdomain.com
```
Delete the certificate locally
```
certbot delete --cert-name yourdomain.com
```
Update nginx after revocation
```
systemctl reload nginx
```
or
```
systemctl restart nginx
```
**SSL certificates and revocation**.

## How certificate revocation works

When you **revoke a certificate** with Certbot:

```bash
sudo certbot revoke --cert-name yourdomain.com
```

* Let’s Encrypt marks the certificate as **revoked** in its **Certificate Revocation List (CRL)**.
* Browsers and clients can check the CRL or use **OCSP (Online Certificate Status Protocol)** to see if the cert is revoked.

---

## Why SSL still works immediately

Even after revocation, the **certificate file is still valid on your server**, and:

* Most browsers **do not check revocation for every HTTPS request**.
* Some clients cache the certificate status.
* Revocation is not like expiration — the certificate is technically still valid until it **expires** (usually 90 days for Let’s Encrypt).

So, your site can still serve HTTPS successfully **until clients see it is revoked** or until it expires.

---

## How long it “works”

* **Technically:** until the certificate’s **expiry date** (Let’s Encrypt certificates last 90 days).
* **Practically:** many browsers will continue to accept it for hours or days because they **don’t immediately check revocation**.
* Only once a browser checks the CRL/OCSP and sees it revoked will it show warnings.

---

## Recommended steps after revocation

If you revoked a certificate because the key is compromised:

1. **Delete the certificate** locally:

   ```bash
   sudo certbot delete --cert-name yourdomain.com
   ```
2. **Issue a new certificate**:

   ```bash
   sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
   ```
3. **Reload NGINX**:

   ```bash
   sudo systemctl reload nginx
   ```

Revocation **does not instantly break HTTPS**. It prevents new clients from trusting it once they check revocation, but servers can still present it until the certificate expires or is replaced.

---

**step-by-step way to immediately stop serving a revoked Certbot SSL certificate** so your HTTPS truly stops working:

---

## Revoke the certificate (if not already done)

```bash
sudo certbot revoke --cert-name yourdomain.com
```

This marks the certificate as revoked in Let’s Encrypt’s system.

---

## Delete the certificate locally

Even after revocation, the certificate files still exist on your server. Delete them to prevent NGINX/Apache from using them:

```bash
sudo certbot delete --cert-name yourdomain.com
```

This removes files under:

```
/etc/letsencrypt/live/yourdomain.com/
```

and related directories.

---

## Update your NGINX or Apache configuration

### NGINX:

* Open your server block:

```bash
sudo nano /etc/nginx/sites-available/default
```

* Remove or comment out the lines pointing to the revoked certificate:

```nginx
ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
```

* Optionally, disable the SSL block entirely or redirect HTTPS to HTTP temporarily.

### Apache:

* Open the virtual host config:

```bash
sudo nano /etc/apache2/sites-available/your-site.conf
```

* Remove or comment out `SSLCertificateFile` and `SSLCertificateKeyFile`.

---

## Reload the web server

### NGINX:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

### Apache:

```bash
sudo apache2ctl configtest
sudo systemctl reload apache2
```

Now the server **will no longer serve the revoked certificate**, and HTTPS will stop working until you install a new certificate.

---

## Optional: Replace with a new certificate

If your goal is to continue HTTPS safely, immediately request a **new certificate**:

```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

This ensures your site uses a valid, trusted certificate.

---

**Key point:**
Revocation alone doesn’t stop HTTPS because the old certificate still exists on your server. You must **delete the certificate files** and **update the web server configuration** to fully stop serving it.
