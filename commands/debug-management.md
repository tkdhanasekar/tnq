## kdump

## 1. **Install kdump utilities**

Most distributions require installing `kdump` and `kexec-tools` (for Red Hat/CentOS) or `linux-crashdump` (for Ubuntu/Debian).

**RHEL/CentOS/Fedora**

```bash
sudo yum install kexec-tools
sudo yum install crash
```

**Ubuntu/Debian**

```bash
sudo apt install kdump-tools crash kexec-tools
```

---

## 2. **Enable the kdump service**

```bash
sudo systemctl enable kdump
sudo systemctl start kdump
```

Check status:

```bash
systemctl status kdump
```

---

## 3. **Configure memory reserved for kdump**

Edit `/etc/default/grub` (Ubuntu) or `/etc/grub.conf` (RHEL/CentOS):

```text
GRUB_CMDLINE_LINUX="crashkernel=512M"
```

Then update GRUB:

**RHEL/CentOS**

```bash
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```

**Ubuntu**

```bash
sudo update-grub
```

---

## 4. **Set the dump location**

Edit `/etc/kdump.conf`:

* To save crash dumps to local disk:

```text
path /var/crash
```

* To save crash dumps to a network location (NFS):

```text
net nfs <server-ip>:/path/to/dump
```

* To save crash dumps to remote SSH server:

```text
ssh user@host:/path/to/dump
```

---

## 5. **Start/Restart kdump service after configuration**

```bash
sudo systemctl restart kdump
```

---

## 6. **Test kdump by triggering a crash**

> ⚠ Warning: This will crash your system. Only test in a VM or safe environment.

```bash
echo c | sudo tee /proc/sysrq-trigger
```

After reboot, check `/var/crash/` (or your configured location) for the dump files.

---

## 7. **Analyze the crash dump**

```bash
sudo crash /usr/lib/debug/lib/modules/$(uname -r)/vmlinux /var/crash/<vmcore>
```

This allows you to inspect kernel state, processes, and call stacks at the time of the crash.

---



