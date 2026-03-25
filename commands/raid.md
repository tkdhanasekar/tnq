<details>
 <summary>raid0</summary>

## Setup RAID 0 on Linux (using mdadm)

## 1. Install required tool

```bash
sudo apt update
sudo apt install mdadm
```

---

## 2. Identify your disks

Check available drives:

```bash
lsblk
```

---

## 3. Create RAID 0 array

```bash
sudo mdadm --create --verbose /dev/md0 --level=0 --raid-devices=2 /dev/sdc /dev/sdd
```

* `/dev/md0` → RAID device name
* `--level=0` → RAID 0
* `--raid-devices=2` → number of disks

---

## 4. Create filesystem

```bash
sudo mkfs.ext4 /dev/md0
```

---

## 5. Mount the RAID

```bash
sudo mkdir /mnt/raid0
sudo mount /dev/md0 /mnt/raid0
```

---

## 6. Make it persistent

Save RAID config:

```bash
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
sudo update-initramfs -u
```

Add to `/etc/fstab`:

```bash
/dev/md0 /mnt/raid0 ext4 defaults,nofail,discard 0 0
```

---

## Check if RAID 0 is working

## 1. Check RAID status

```bash
cat /proc/mdstat
```

You should see something like:

```
md0 : active raid0 sdb[0] sdc[1]
```

---

## 2. Detailed RAID info

```bash
sudo mdadm --detail /dev/md0
```

Look for:

* `Raid Level : raid0`
* Both disks listed as **active**

---

## 3. Test performance (important for RAID 0)

```bash
sudo apt install hdparm
sudo hdparm -Tt /dev/md0
```

Or better:

```bash
dd if=/dev/zero of=/mnt/raid0/testfile bs=1G count=1 oflag=direct
```

You should see **higher speed than a single disk**

---

## 4. Check mounted filesystem

```bash
df -h
```

You should see combined disk size

---

## Important warnings

* RAID 0 = **NO redundancy**
* If **one disk fails → all data lost**
* Always use for:

  * Temporary data
  * Performance workloads
  * Not critical storage
</details>
<details>
 <summary>raid1</summary>
 
Setting up **RAID 1 (mirroring)** means duplicating data across two drives so if one fails, the other still has everything. I’ll walk you through both **setup** and **verification**, mainly on Linux (most common), and briefly mention other environments.

---

## 1. RAID 1 Setup (Linux using `mdadm`)

## Step 1: Install required tool

```bash
sudo apt update
sudo apt install mdadm
```

---

## Step 2: Identify disks

```bash
lsblk
```

Example disks:

* `/dev/sdc`
* `/dev/sdd`

---

## Step 3: Create RAID 1 array

```bash
sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdc /dev/sdd
```

---

## Step 4: Check RAID status (initial sync)

```bash
cat /proc/mdstat
```

You’ll see something like:

```
md0 : active raid1 sdb[0] sdc[1]
      [2/2] [UU]
```

* `UU` = both disks working
* Sync may take time

---

## Step 5: Create filesystem

```bash
sudo mkfs.ext4 /dev/md0
```

---

## Step 6: Mount RAID

```bash
sudo mkdir /mnt/raid1
sudo mount /dev/md0 /mnt/raid1
```

---

## Step 7: Save configuration (important!)

```bash
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
sudo update-initramfs -u
```

---

## 2. How to Check RAID 1 is Working

## Method 1: Check status

```bash
cat /proc/mdstat
```

Healthy output:

```
[UU]
```

---

## Method 2: Detailed info

```bash
sudo mdadm --detail /dev/md0
```

Look for:

* `State : clean`
* `Active Devices : 2`
* `Working Devices : 2`

---

## Method 3: Test fault tolerance

Simulate disk failure:

```bash
sudo mdadm --fail /dev/md0 /dev/sdc
```

Check status again:

```bash
cat /proc/mdstat
```

Now you should see:

```
[U_]
```

This proves RAID is working — one disk failed but system still runs.

---

## Method 4: Remove and re-add disk

```bash
sudo mdadm --remove /dev/md0 /dev/sdc
sudo mdadm --add /dev/md0 /dev/sdc
```

Watch rebuild:

```bash
cat /proc/mdstat
```

---

## Key Concepts

* RAID 1 = **100% redundancy, 50% usable capacity**
* If 2 × 1TB → usable = 1TB
* Reads are faster, writes slightly slower
* Protects against **disk failure**, NOT:

  * accidental deletion
  * viruses
  * corruption

---

## Common Mistakes

* Using disks with existing partitions
* Forgetting to save mdadm config
* Not testing failure scenario
* Assuming RAID = backup (it is NOT)

---

## Quick Health Checklist

* `[UU]` in `/proc/mdstat`
* No degraded state 
* Rebuild works after disk failure
</details>
