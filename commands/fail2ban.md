update the server
```
apt update
```
Install Fail2Ban
```
apt install fail2ban -y
```
start, enable and check status
```
systemctl start fail2ban && systemctl enable fail2ban && systemctl status fail2ban --no-pager
```
add parameters to the
```
vim /etc/fail2ban/jail.local
```
```
bantime = 1h
findtime = 10m
maxretry = 5
backend = systemd


[sshd]
enabled = true
port = ssh
logpath = %(sshd_log)s
```
:wq!
```
systemctl restart fail2ban
```
Check Status: 
```
sudo fail2ban-client status
```
Check SSH Jail Status: 
```
fail2ban-client status sshd
```
Optional: Whitelist Your IP 
Add your trusted IP so you don’t lock yourself out:

Edit jail.local:
```
ignoreip = 127.0.0.1/8 YOUR_PUBLIC_IP
```
```
systemctl restart fail2ban
```
Ban an IP manually:
```
sudo fail2ban-client set sshd banip 1.2.3.4
```
Unban an IP:
```
sudo fail2ban-client set sshd unbanip 1.2.3.4
```
restart the service
```
systemctl restart fail2ban
```
Check logs:
```
sudo journalctl -u fail2ban
```
For very high-security environments:
```
bantime = -1   # Permanent ban
```
Verify fail2ban Works
```
systemctl is-active fail2ban
```
