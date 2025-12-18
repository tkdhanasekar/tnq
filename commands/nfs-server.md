On the **Server system**:
## 1. Update the system

```bash
sudo apt update
```

---

## 2. Install NFS server packages

```bash
sudo apt install nfs-kernel-server -y
```

Verify installation:

```bash
systemctl status nfs-server
```

---

## 3. Create a directory to share

Example: sharing `/mnt/nfsdir`

```bash
sudo mkdir -p /mnt/nfsdir
```

Set permissions:

```bash
sudo chown nobody:nogroup /mnt/nfsdir
sudo chmod 777 /mnt/nfsdir
```

For production, use more restrictive permissions.

---

## 4. Configure NFS exports

Edit the exports file:

```bash
sudo vim /etc/exports
```
```bash
/mnt/nfsdir client_server_ip(rw,sync,no_subtree_check)
```

### Common export options explained:

* `rw` – Read/write access
* `sync` – Write changes to disk immediately (safer)
* `no_subtree_check` – Improves reliability
* `ro` – Read-only (optional)
* `no_root_squash` – Allows root access (insecure, avoid unless needed)

---

## 5. Apply export configuration

```bash
sudo exportfs -a
```

Verify:

```bash
sudo exportfs -v
```

---

## 6. Start and enable NFS services

```bash
sudo systemctl restart nfs-server
sudo systemctl enable nfs-server
```
---

## 8. Install NFS client on another machine

On the **client system**:

```bash
sudo apt install nfs-common -y
```

---

## 9. Mount NFS share on the client

Create mount point:

```bash
sudo mkdir -p /mnt/nfsdir_client
```

Mount manually:

```bash
sudo mount NFS_SERVER_IP:/mnt/nfsdir /mnt/nfsdir_client
```
Verify:

```bash
df -h
```

---

## 10. Permanent mount (optional)

Edit `/etc/fstab` on the client:

```bash
sudo vim /etc/fstab
```

Add:

```bash
NFS_SERVER_IP:/mnt/nfsdir /mnt/nfsdir_client nfs defaults 0 0
```

Test:

```bash
sudo mount -a
```

---

## 11. Test the setup

On the client:

```bash
cd /mnt/nfsdir_client
touch testfile
```
check in nfs server
```
cd /mnt/nfsdir
ls
```
create a file in nfs-server
```
cd /mnt/nfsdir
touch examplefile
```
check in nfs-client
```
cd /mnt/nfsdir_client
ls
```
