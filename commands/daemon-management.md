### 1. Start a Service

Start a service immediately (does not enable on boot).

```bash
sudo systemctl start nginx
```

Example:

```bash
sudo systemctl start sshd
```

---

### 2. Stop a Service

Stop a running service.

```bash
sudo systemctl stop nginx
```

Example:

```bash
sudo systemctl stop apache2
```

---

### 3. Restart a Service

Stop and then start the service again.

```bash
sudo systemctl restart nginx
```

Example:

```bash
sudo systemctl restart docker
```

---

### 4. Reload a Service

Reload configuration without stopping the service (if supported).

```bash
sudo systemctl reload nginx
```

Example:

```bash
sudo systemctl reload sshd
```

---

### 5. Check Service Status

Show current status (running, failed, etc.).

```bash
systemctl status nginx
```

Example:

```bash
systemctl status firewalld
```

---

### 6. Enable a Service (Start at Boot)

Enable service to start automatically at boot.

```bash
sudo systemctl enable nginx
```

Example:

```bash
sudo systemctl enable docker
```

---

### 7. Disable a Service

Prevent service from starting at boot.

```bash
sudo systemctl disable nginx
```

Example:

```bash
sudo systemctl disable bluetooth
```

---

### 8. Check if Service is Enabled

```bash
systemctl is-enabled nginx
```

Example:

```bash
systemctl is-enabled sshd
```

---

### 9. Check if Service is Active

```bash
systemctl is-active nginx
```

Example:

```bash
systemctl is-active mysql
```

---

### 10. List All Running Services

```bash
systemctl list-units --type=service
```

---

### 11. List All Services (Including Inactive)

```bash
systemctl list-units --type=service --all
```

---

### 12. List Unit Files

Shows installed service files.

```bash
systemctl list-unit-files --type=service
```

---

### 13. Mask a Service

Completely prevent a service from starting (even manually).

```bash
sudo systemctl mask nginx
```

---

### 14. Unmask a Service

Allow a masked service to be started.

```bash
sudo systemctl unmask nginx
```

---

### 15. Reboot System

```bash
sudo systemctl reboot
```

---

### 16. Power Off System

```bash
sudo systemctl poweroff
```

---

### 17. Suspend System

```bash
sudo systemctl suspend
```

---

### 18. Reload systemd Manager Configuration

After editing unit files:

```bash
sudo systemctl daemon-reload
```

---

If you create a service file:

```
/etc/systemd/system/myapp.service
```

Typical workflow:

```bash
sudo systemctl daemon-reload
sudo systemctl start myapp
sudo systemctl enable myapp
systemctl status myapp
```

### 19. To List active units
```
sudo systemctl list-units
```

### 20. To List all units
```
sudo systemctl list-units --all
```

### 21. To List installed unit files
```
sudo systemctl list-unit-files
```

### 22. To List sockets
```
sudo systemctl list-sockets
```

### 23. To list dependencies
```
systemctl list-dependencies <unit>
```

### 24. To Show detailed properties
```
sudo systemctl show <service>
```

### 25. To Show unit file content
```
sudo systemctl cat <service>
```

### 26. To show help
```
sudo systemctl --help
```

### 27. To Show help for a service
```
sudo systemctl help apache2
```

### 28. Service Log Inspection
```
journalctl -u <service>
```
```
journalctl -xe
```

### 29. To Re-execute systemd process
```
sudo systemctl daemon-reexec
```

### 30. To Reset and re-enable
```
sudo systemctl reenable <service>
```
