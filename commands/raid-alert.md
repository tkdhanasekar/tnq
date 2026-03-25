To monitor **RAID health automatically with email alerts**, you can use `mdadm`’s built-in monitoring service. This will notify you if a disk fails, array degrades, or rebuild starts.

Here’s a clean, practical setup 👇

---

# 1. Install Mail Utility

You need a mail system to send alerts.

### Option A (simple, works on most systems):

```bash
sudo apt install mailutils
```

### Option B (more robust):

```bash
sudo apt install postfix
```

During Postfix setup:

* Choose **“Internet Site”**
* Enter your server hostname

---

# 2. Configure mdadm Email Alerts

Edit config:

```bash
sudo nano /etc/mdadm/mdadm.conf
```

Add or modify this line:

```bash
MAILADDR your-email@example.com
```

Optional (recommended):

```bash
MAILFROM raid-monitor@yourserver.com
```

---

# 3. Enable mdadm Monitoring Service

Start monitoring daemon:

```bash
sudo systemctl enable mdadm --now
```

Or manually run:

```bash
sudo mdadm --monitor --scan --daemonise
```

---

# 4. Test Email Alerts (IMPORTANT)

Simulate a disk failure:

```bash
sudo mdadm /dev/md0 --fail /dev/sdb1
```

You should receive an email like:

* “DegradedArray”
* “Fail event detected”

After testing, re-add disk:

```bash
sudo mdadm /dev/md0 --remove /dev/sdb1
sudo mdadm /dev/md0 --add /dev/sdb1
```

---

# 5. Check Logs (if no email received)

```bash
sudo journalctl -u mdadm
```

Or:

```bash
sudo dmesg | grep md
```

---

# 6. (Optional) Use External SMTP (Gmail, etc.)

If emails aren’t sending (common on cloud/VPS), configure Postfix with SMTP relay.

Example (Gmail SMTP):

Edit:

```bash
sudo nano /etc/postfix/main.cf
```

Add:

```bash
relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_tls_security_level = encrypt
```

Create credentials:

```bash
sudo nano /etc/postfix/sasl_passwd
```

Add:

```
[smtp.gmail.com]:587 your-email@gmail.com:app-password
```

Then:

```bash
sudo postmap /etc/postfix/sasl_passwd
sudo systemctl restart postfix
```

---

# 7. What Alerts You’ll Get

* Disk failure ⚠️
* Array degraded
* Rebuild started/completed
* Spare activated

---

# Pro Tips

* Use a **dedicated alert email** (not personal inbox)
* Combine with:

  * `smartctl` (disk health monitoring)
  * Cron checks for `/proc/mdstat`

Example cron check:

```bash
*/5 * * * * cat /proc/mdstat | grep -q "\[UU\]" || echo "RAID issue!" | mail -s "RAID ALERT" you@example.com
```

---

# Common Issues

* No email → SMTP not configured
* Gmail blocked → use **App Password**, not normal password
* Firewall blocking port 25/587
