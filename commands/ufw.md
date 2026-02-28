## Install & Enable

```bash
sudo apt install ufw        # Install UFW
sudo ufw enable             # Enable firewall
sudo ufw disable            # Disable firewall
sudo ufw status             # Show status
sudo ufw status verbose     # Detailed status
```

---

## Default Policies

```bash
sudo ufw default deny incoming    # Block all incoming by default
sudo ufw default allow outgoing   # Allow all outgoing by default
sudo ufw default deny outgoing    # (Optional) Block outgoing by default
```

---

## Allow Connections

### Allow by Port

```bash
sudo ufw allow 22          # Allow SSH
sudo ufw allow 80          # Allow HTTP
sudo ufw allow 443         # Allow HTTPS
sudo ufw allow 8080        # Custom port
```

### Allow Specific Protocol

```bash
sudo ufw allow 53/tcp
sudo ufw allow 53/udp
```

### Allow Port Range

```bash
sudo ufw allow 6000:6007/tcp
```

### Allow from Specific IP

```bash
sudo ufw allow from 192.168.1.100
sudo ufw allow from 192.168.1.100 to any port 22
```

### Allow Specific Subnet

```bash
sudo ufw allow from 192.168.1.0/24
```

---

## Deny / Reject Rules

```bash
sudo ufw deny 23                # Block Telnet
sudo ufw deny from 192.168.1.50
sudo ufw reject 25             
```

---

## Delete Rules

### By Rule Number

```bash
sudo ufw status numbered        # Show numbered rules
sudo ufw delete 3               # Delete rule #3
```

### By Full Rule

```bash
sudo ufw delete allow 80
```

---

## Application Profiles

List available app profiles:

```bash
sudo ufw app list
```

Allow app profile:

```bash
sudo ufw allow OpenSSH
```

Show profile details:

```bash
sudo ufw app info OpenSSH
```

---

## Logging

```bash
sudo ufw logging on
sudo ufw logging off
sudo ufw logging low|medium|high|full
```

Logs are typically in:

```bash
/var/log/ufw.log
```

---

## Reload / Reset

```bash
sudo ufw reload     # Reload rules
sudo ufw reset      # Reset everything (disables UFW)
```

---

# Common Server Setup Example

Typical web server setup:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```
