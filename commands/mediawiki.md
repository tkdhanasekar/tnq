## 1. Update your system

Always a good warm-up:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install the LAMP stack

### Install Apache

```bash
sudo apt install apache2 -y
sudo systemctl enable --now apache2
```

Check it:

* Open `http://your_server_ip/`
* You should see the Apache default page

---

### Install MariaDB (MySQL-compatible)

```bash
sudo apt install mariadb-server mariadb-client -y
sudo systemctl enable --now mariadb
```

Secure it:

```bash
sudo mysql_secure_installation
```

Recommended answers:

* Set root password: **Yes**
* Remove anonymous users: **Yes**
* Disallow remote root login: **Yes**
* Remove test database: **Yes**
* Reload privileges: **Yes**

---

### Install PHP + required extensions

MediaWiki is picky about extensions, so install these upfront:

```bash
sudo apt install php php-apcu php-intl php-mbstring php-xml php-mysql php-gd php-curl php-cli php-zip -y
```

Verify PHP:

```bash
php -v
```

---

## 3. Create the MediaWiki database

Log into MariaDB:

```bash
sudo mysql -u root -p
```

Run these SQL commands (change names/passwords):

```sql
CREATE DATABASE mediawiki;
CREATE USER 'wikiuser'@'localhost' IDENTIFIED BY 'strong_password_here';
GRANT ALL PRIVILEGES ON mediawiki.* TO 'wikiuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

## 4. Download MediaWiki

Go to `/var/www`:

```bash
cd /var/www
```

Download the latest stable release:

```bash
sudo wget https://releases.wikimedia.org/mediawiki/1.41/mediawiki-1.41.3.tar.gz
```

Extract and rename:

```bash
sudo tar -xvzf mediawiki-1.41.3.tar.gz
sudo mv mediawiki-1.41.3 mediawiki
```

Set permissions:

```bash
sudo chown -R www-data:www-data /var/www/mediawiki
sudo chmod -R 755 /var/www/mediawiki
```

---

## 5. Configure Apache for MediaWiki

Create a virtual host:

```bash
sudo nano /etc/apache2/sites-available/mediawiki.conf
```

Paste this (adjust domain if needed):

```apache
<VirtualHost *:80>
    ServerName wiki.example.com
    DocumentRoot /var/www/mediawiki

    <Directory /var/www/mediawiki>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/mediawiki_error.log
    CustomLog ${APACHE_LOG_DIR}/mediawiki_access.log combined
</VirtualHost>
```

Enable the site and rewrite module:

```bash
sudo a2ensite mediawiki.conf
sudo a2enmod rewrite
sudo systemctl reload apache2
```

---

## 6. Run the MediaWiki web installer

Open your browser:

```
http://your_server_ip/
```

or

```
http://wiki.example.com/
```

You’ll see the **MediaWiki installer**.

### During setup:

* Database type: **MariaDB / MySQL**
* Database name: `mediawiki`
* Database user: `wikiuser`
* Database password: your password
* Database host: `localhost`
* Table prefix: (leave empty unless you want one)
* Create admin account
* Wiki name: your choice

Finish the installer.

---

## 7. Finalize installation

The installer will give you a file called:

```
LocalSettings.php
```

Move it into place:

```bash
sudo mv ~/Downloads/LocalSettings.php /var/www/mediawiki/
sudo chown www-data:www-data /var/www/mediawiki/LocalSettings.php
```

---

## 8. (Optional but recommended) Enable uploads

Edit `LocalSettings.php`:

```bash
sudo nano /var/www/mediawiki/LocalSettings.php
```

Add:

```php
$wgEnableUploads = true;
```

Restart Apache:

```bash
sudo systemctl restart apache2
```
