**LetsEncrypt SSL revoke for Nginx**
```
sudo certbot revoke --cert-name yourdomain.com && \
sudo certbot delete --cert-name yourdomain.com && \
sudo sed -i '/ssl_certificate/d;/ssl_certificate_key/d' /etc/nginx/sites-available/default && \
sudo nginx -t && sudo systemctl reload nginx
```
**LetsEncrypt SSL revoke for Apache**

```
sudo certbot revoke --cert-name yourdomain.com && \
sudo certbot delete --cert-name yourdomain.com && \
sudo sed -i '/SSLCertificateFile/d;/SSLCertificateKeyFile/d' /etc/apache2/sites-available/000-default.conf && \
sudo apache2ctl configtest && sudo systemctl reload apache2
```

Make a backup of old config files
For nginx
```
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default.bak
```
For Apache
```
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf.bak
```
