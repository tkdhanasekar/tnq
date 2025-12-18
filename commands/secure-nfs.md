Below are **recommended `/etc/exports` parameters for a *production-grade, secure NFS setup***, with explanations and examples you can safely use in real environments.

---

## 1. Core security principles for production NFS

In production, you should:

* Restrict access to **specific IPs or subnets**
* Avoid `no_root_squash`
* Use **read-only** where possible
* Minimize privileges
* Prefer **NFSv4**
* Use strong file permissions + proper ownership

---

## 2. Secure & recommended `/etc/exports` options

### ✅ Standard secure production export (most common)

```bash
/srv/nfs_share 192.168.1.20(rw,sync,no_subtree_check,root_squash)
```

### Explanation:

| Option             | Purpose                                          |
| ------------------ | ------------------------------------------------ |
| `rw`               | Allows read/write access                         |
| `sync`             | Writes are committed to disk immediately (safer) |
| `no_subtree_check` | Prevents stale file handle errors                |
| `root_squash`      | Maps client root → nobody (security critical)    |

> `root_squash` is **ON by default**, but explicitly setting it is best practice.

---

## 3. Read-only export (highest security)

```bash
/srv/nfs_share 192.168.1.0/24(ro,sync,no_subtree_check,root_squash)
```

✔ Ideal for application binaries, ISO images, or static data.

---

## 4. Multiple clients with different permissions

```bash
/srv/nfs_share 192.168.1.10(rw,sync,root_squash) 192.168.1.11(ro,sync,root_squash)
```

---

## 5. Map all users to a specific non-privileged user

Very secure for shared uploads.

```bash
/srv/nfs_share 192.168.1.0/24(rw,sync,all_squash,anonuid=65534,anongid=65534)
```

### When to use:

* Public upload directories
* Shared scratch space
* Prevents privilege abuse

---

## 6. Options to **AVOID in production**

🚫 **Do NOT use unless absolutely required**

```bash
no_root_squash
```

**Why dangerous?**

* Client root gets full root access on server
* Massive security risk

---

## 7. Secure permissions on the shared directory

### Recommended ownership

```bash
sudo chown -R nfsuser:nfsgroup /srv/nfs_share
sudo chmod 750 /srv/nfs_share
```

### Why:

* Limits access to intended users
* Prevents world-writable shares (`777` is insecure)

---

## 8. Enforcing NFSv4 only (recommended)

Edit:

```bash
sudo nano /etc/default/nfs-kernel-server
```

Set:

```bash
RPCNFSDOPTS="--nfs-version 4"
```

Restart:

```bash
sudo systemctl restart nfs-server
```

---

## 9. Example: **Enterprise-grade secure `/etc/exports`**

```bash
/srv/nfs_share 192.168.10.0/24(rw,sync,no_subtree_check,root_squash)
```

With:

* Firewall restricted to port 2049
* Strong Linux permissions
* NFSv4 enforced

---

## 10. Apply & verify

```bash
sudo exportfs -ra
sudo exportfs -v
```

---

## 11. Quick security checklist ✅

* [ ] No `no_root_squash`
* [ ] No `777` permissions
* [ ] IP-restricted access
* [ ] NFSv4 only
* [ ] Firewall enabled
* [ ] Read-only where possible

---

### If you want, I can also provide:

* **Kerberos-secured NFS (enterprise level)**
* **Audit checklist for production NFS**
* **RHCSA / Linux admin exam notes**

Just tell me 👍

=================================================

### What is `no_root_squash` in NFS?

`no_root_squash` is an **NFS export option** that **disables a major security protection** and allows the **root user on an NFS client to act as root on the NFS server** for that shared directory.

---

## Default behavior (secure)

By default, NFS uses **`root_squash`**.

### `root_squash`

* Client **root (UID 0)** is mapped to **`nobody` / `nogroup`** on the server
* Prevents root on a client from modifying sensitive files on the server
* **Protects the server from privilege escalation**

---

## What `no_root_squash` does

When you use:

```bash
no_root_squash
```

It means:

* Client root user **keeps UID 0**
* Client root has **full root privileges** on the exported directory
* Can:

  * Change ownership (`chown`)
  * Modify permissions
  * Delete or replace files
  * Potentially compromise the server

---

## Example

```bash
/srv/nfs_share 192.168.1.20(rw,sync,no_root_squash)
```

🔴 **Result:**
If the client runs:

```bash
sudo rm -rf /mnt/nfs_share/*
```

Those files are deleted **as root on the server**.

---

## Why it is dangerous (production risk)

* Any compromised client = compromised server data
* Breaks trust boundary
* Violates least-privilege principle
* Common cause of NFS security breaches

---

## When (rarely) it is acceptable

Use `no_root_squash` **ONLY** when:

* You fully trust the client
* Isolated network (e.g., private VM lab)
* Specific use cases like:

  * Diskless clients
  * Backup servers
  * Certain HPC clusters

Even then → **use with caution**

---

## Secure alternatives

### ✔ Use default `root_squash`

```bash
/srv/nfs_share 192.168.1.20(rw,sync,root_squash)
```

### ✔ Use `all_squash`

Maps *all* users to a non-privileged user:

```bash
all_squash,anonuid=65534,anongid=65534
```

---

## Quick summary

| Option           | Effect                                 |
| ---------------- | -------------------------------------- |
| `root_squash`    | Client root → nobody (secure, default) |
| `no_root_squash` | Client root = server root (insecure)   |
| `all_squash`     | All users → nobody (most restrictive)  |

---

### One-line exam answer (RHCSA / admin):

> **`no_root_squash` allows the root user on an NFS client to have root privileges on the NFS server, which is insecure and should be avoided in production.**

If you want, I can also explain **UID/GID mapping**, **`anonuid/anongid`**, or **real-world attack examples**.


