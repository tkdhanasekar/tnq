update the server
```
apt update
```
install apache
```
apt install apache2 -y
```
start, enable, check status
```
systemctl start apache2 && systemctl enable apache2 && systemctl status apache2 --no-pager
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
<h1>Apache Webserver Test Page</h1>
```
save and exit
restart the apache service
```
systemctl restart apache2
```
Test Apache’s configuration files for syntax errors using
```
apache2 -t
```
check in browser
http://url

**LetsEncrypt SSL certificate for apache webserver**
install packages
```
apt install certbot python3-certbot-apache
```
```
certbot --apache -d yourdomain.com
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
Revoke by domain name
```
certbot revoke --cert-name yourdomain.com
```
Delete the certificate locally
```
certbot delete
```
Update Apache after revocation
```
systemctl reload apache2
```
or
```
systemctl restart apache2
```
