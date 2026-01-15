<details>
 <summary>du</summary>

1. **Check disk usage of the current directory**

```
du
```

2. **Show disk usage in human-readable format (KB, MB, GB)**

```
du -h
```

3. **Check disk usage of a specific directory**

```
du -h /var/log
```

4. **Show disk usage of all files and directories (not just directories)**

```
du -ah
```

5. **Display only the total size of a directory**

```
du -sh /home/user
```

6. **Show disk usage for each subdirectory (one level deep)**

```
du -h --max-depth=1 /home
```

7. **Sort directories by size (largest first)**

```
du -h --max-depth=1 | sort -hr
```

8. **Exclude specific directories**

```
du -h --exclude=cache
```

9. **Check disk usage using a specific block size**

```
du -h --block-size=1G
```

10. **Summarize disk usage of multiple directories**

```
du -sh /etc /usr /var
```
11. **To find the top 10 biggest files using du for the entire system**
```
sudo du -ah / | sort -hr | head -n 10
```
</details>
<details>
 <summary>df</summary>
 
1. **Show disk space usage for all mounted filesystems**

```
df
```

2. **Display disk usage in human-readable format (KB, MB, GB)**

```
df -h
```

3. **Show disk usage in human-readable format using powers of 1000**

```
df -H
```

4. **Show disk usage for a specific directory**

```
df /home
```

5. **Show disk usage including filesystem type**

```
df -T
```

6. **Show disk usage for all filesystems, including dummy (pseudo) filesystems**

```
df -a
```

7. **Display disk usage in kilobytes**

```
df -k
```

8. **Display disk usage in megabytes**

```
df -m
```

9. **Exclude specific filesystem types (for example, tmpfs)**

```
df -x tmpfs
```

10. **Display inode usage instead of block usage**

```
df -i
```
</details>
<details>
 <summary>fallocate</summary>

1. **Create a file of a specific size (1 GB)**

```
fallocate -l 1G myfile.img
```

2. **Create a file of 500 MB**

```
fallocate -l 500M datafile.bin
```

3. **Create a file of 10 MB**

```
fallocate -l 10M testfile.txt
```

4. **Create a file using bytes**

```
fallocate -l 1048576 one_mb_file
```

5. **Extend an existing file to 2 GB**

```
fallocate -l 2G existingfile.log
```

6. **Create a sparse file (no actual blocks allocated)**

```
fallocate -s -l 1G sparsefile.img
```

7. **Punch holes in a file (free space in the middle of a file)**

```
fallocate -p -o 100M -l 200M bigfile.dat
```

8. **Reserve disk space without initializing data**

```
fallocate -n -l 300M reservedfile.bin
```

9. **Collapse a range of a file (remove space from the middle)**

```
fallocate -c -o 50M -l 100M logfile.txt
```

10. **Insert space into a file at a specific offset**

```
fallocate -i -o 20M -l 50M report.txt
```
</details>
<details>
 <summary>dd</summary>

1. **Create a file of a specific size filled with zeros**

```
dd if=/dev/zero of=output.img bs=1M count=100
```

*Creates a 100 MB file called `output.img`.*

---

2. **Copy a disk or partition**

```
dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

*Clones the contents of `/dev/sda` to `/dev/sdb`.*

---

3. **Create a bootable USB from an ISO**

```
dd if=linux.iso of=/dev/sdb bs=4M status=progress
```

*Writes `linux.iso` directly to a USB drive (`/dev/sdb`).*

---

4. **Backup the MBR (first 512 bytes)**

```
dd if=/dev/sda of=mbr_backup.bin bs=512 count=1
```

*Backs up the Master Boot Record of `/dev/sda`.*

---

5. **Convert file format to ASCII or EBCDIC**

```
dd if=input.txt of=output.txt conv=ascii
```

*Converts the file encoding to ASCII.*

---

6. **Create a file of random data**

```
dd if=/dev/urandom of=random.bin bs=1M count=10
```

*Generates a 10 MB file of random data.*

---

7. **Wipe a disk with zeros**

```
dd if=/dev/zero of=/dev/sdc bs=1M status=progress
```

*Completely clears `/dev/sdc`.*

---

8. **Wipe a disk with random data**

```
dd if=/dev/urandom of=/dev/sdc bs=1M status=progress
```

*Securely overwrites `/dev/sdc` with random data.*

---

9. **Copy a file with block size conversion**

```
dd if=input.img of=output.img bs=512 conv=sync,noerror
```

*Copies a file using 512-byte blocks, filling missing blocks with zeros and ignoring errors.*

---

10. **Benchmark write speed of a disk**

```
dd if=/dev/zero of=testfile bs=1G count=1 oflag=direct
```

*Writes a 1 GB file directly to disk to test speed.*
</details>
<details>
 <summary>create-swap</summary>

To add 4G swap space
preallocate space to a file
```
sudo fallocate -l 4G /swapfile
```
change the permission
```
sudo chmod 600 /swapfile
```
make the swap file
```
sudo mkswap /swapfile
```
enable devices and files for paging and swapping
```
sudo swapon /swapfile
```
for persistent swap space add these parameters to fstab file
```
sudo vim /etc/fstab
```
```
/swapfile swap swap defaults 0 0
```
:wq! save and exit
```
sudo swapon --show
```
check with free command
```
free -h
```
</details>
<details>
 <summary>swap-commands</summary>

### **1. View swap usage**

* **Check total swap and usage**

```
swapon --show
```

```
free -h
```

```
cat /proc/swaps
```

---

### **2. Enable swap**

* **Turn on a swap partition or file**

```
sudo swapon /swapfile
```

---

### **3. Disable swap**

* **Turn off a swap partition or file**

```
sudo swapoff /swapfile
```

---

### **4. Create a swap file**

* **Allocate a swap file of 1 GB**

```
sudo fallocate -l 1G /swapfile
```

* **Or using `dd`**

```
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
```

---

### **5. Set permissions for swap file**

```
sudo chmod 600 /swapfile
```

---

### **6. Format a file as swap**

```
sudo mkswap /swapfile
```

---

### **7. Make swap permanent (auto-mount at boot)**

* **Add entry to `/etc/fstab`**

```
/swapfile none swap sw 0 0
```

---

### **8. Adjust swap usage priority**

* **Check priority of swap devices**

```
cat /proc/swaps
```

* **Set priority when enabling swap**

```
sudo swapon --priority 10 /swapfile
```

---

### **9. Change swappiness**

* **View current swappiness (how aggressively Linux uses swap)**

```
cat /proc/sys/vm/swappiness
```

* **Temporarily set swappiness**

```
sudo sysctl vm.swappiness=10
```

* **Make it permanent**

```
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

---

### **10. Remove swap file safely**

```
sudo swapoff /swapfile
sudo rm /swapfile
```
</details>
<details>
 <summary>swapon</summary>

1. **Show all active swap devices and files**

```
swapon --show
```

2. **Enable a swap file**

```
sudo swapon /swapfile
```

3. **Enable a swap partition**

```
sudo swapon /dev/sda2
```

4. **Enable multiple swap files at once**

```
sudo swapon /swapfile1 /swapfile2
```

5. **Enable a swap file with priority**

```
sudo swapon --priority 10 /swapfile
```

6. **Enable a swap file and display summary**

```
sudo swapon -s
```

*Note: `swapon -s` is legacy but still widely used.*

7. **Check swap usage in human-readable format**

```
swapon --show=NAME,SIZE,USED,PRIO
```

8. **Enable swap with verbose output**

```
sudo swapon -v /swapfile
```

9. **Enable all swap entries listed in `/etc/fstab`**

```
sudo swapon -a
```

10. **Enable swap on a device with a specific filesystem type**

```
sudo swapon --fstype=swap /dev/sdb1
```
</details>
<details>
 <summary>swapoff</summary>

1. **Turn off a specific swap file**

```
sudo swapoff /swapfile
```

2. **Turn off a specific swap partition**

```
sudo swapoff /dev/sda2
```

3. **Turn off all swap devices listed in `/etc/fstab`**

```
sudo swapoff -a
```

4. **Turn off swap and show verbose output**

```
sudo swapoff -v /swapfile
```

5. **Turn off swap for multiple files or partitions**

```
sudo swapoff /swapfile1 /swapfile2
```

6. **Temporarily disable swap before resizing a swap file**

```
sudo swapoff /swapfile
sudo fallocate -l 2G /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

7. **Turn off all swap devices without reading `/etc/fstab`**

```
sudo swapoff --all
```

8. **Turn off a swap partition and monitor with `free`**

```
sudo swapoff /dev/sda2
free -h
```

9. **Disable swap on a device with verbose and debug info**

```
sudo swapoff -v /dev/sdb1
```

10. **Turn off swap temporarily for system performance testing**

```
sudo swapoff -a
```

*Then turn it back on with `sudo swapon -a`.*
</details>
<details>
 <summary>create-partition</summary>

## 1. List available disks

First, identify the disk you want to partition.

```bash
lsblk
```

or

```bash
sudo fdisk -l
```

Example disks:

* `/dev/sda` → main hard disk
* `/dev/sdb` → secondary disk or USB

---

## 2. Open the disk with fdisk

Replace **`/dev/sdb`** with your actual disk name

```bash
sudo fdisk /dev/sdb
```

You’ll enter the interactive `fdisk` prompt.

---

## 3. View existing partitions (optional)

Inside `fdisk`, type:

```
p
```

This prints the current partition table.

---

## 4. Create a new partition

Type:

```
n
```

Then follow the prompts:

1. **Partition type**

   * `p` → primary
   * `e` → extended (MBR only)

2. **Partition number**

   * Usually press **Enter** to accept default

3. **First sector**

   * Press **Enter** to accept default

4. **Last sector / size**

   * Press **Enter** to use remaining space
   * OR specify size, e.g.:

     ```
     +10G
     ```

---

## 5. (Optional) Change partition type

For example, to set Linux filesystem type:

```
t
```

Then enter the partition number and type code (e.g., `83` for Linux).

---

## 6. Verify the partition

Check your changes before saving:

```
p
```

---

## 7. Write changes to disk

To save and exit:

```
w
```

> If you want to cancel without saving, use:
>
> ```
> q
> ```

---

## 8. Inform the kernel of changes

Run:

```bash
sudo partprobe
```

or reboot if the partition doesn’t appear.

---

## 9. Format the new partition

Example: formatting as **ext4**

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

## 10. Mount the partition

```bash
sudo mkdir /mnt/mydisk
sudo mount /dev/sdb1 /mnt/mydisk
```
check with
```
df -Th
```
---

## Common fdisk commands (cheat sheet)

| Command | Description           |
| ------- | --------------------- |
| `n`     | New partition         |
| `p`     | Print partition table |
| `d`     | Delete partition      |
| `t`     | Change partition type |
| `w`     | Write changes         |
| `q`     | Quit without saving   |
| `m`     | Help                  |
</details>
<details>
 <summary>delete-partition</summary>

To delete the partition **`/dev/sdb1`**

## 1. Make sure the partition is unmounted

Check:

```bash
lsblk
```

If it’s mounted, unmount it:

```bash
sudo umount /dev/sdb1
```

---

## 2. Open the disk with fdisk

You must open the **disk**, not the partition:

```bash
sudo fdisk /dev/sdb
```

---

## 3. Delete the partition

Inside the `fdisk` prompt:

1. Type:

   ```
   d
   ```
2. If prompted, enter the partition number:

   ```
   1
   ```

---

## 4. Verify the change

Check the partition table:

```
p
```

Make sure `/dev/sdb1` is gone.

---

## 5. Write changes to disk

Save and exit:

```
w
```

> To cancel without saving, use:
>
> ```
> q
> ```

---

## 6. Reload partition table

```bash
sudo partprobe
```

(or reboot if needed)

---

## 7. Confirm deletion

```bash
lsblk
```

or

```bash
sudo fdisk -l /dev/sdb
```
check with
```
df -Th
```
</details>
<details>
 <summary>lsblk</summary>
 
**`lsblk`** is a Linux command that lists information about block devices (disks, partitions, and logical volumes) in a tree-like format.

1. **Basic usage – list all block devices**

   ```bash
   lsblk
   ```

2. **Show filesystem type and UUID**

   ```bash
   lsblk -f
   ```

3. **Display device sizes in bytes**

   ```bash
   lsblk -b
   ```

4. **List only disks (exclude partitions)**

   ```bash
   lsblk -d
   ```

5. **Show mount points**

   ```bash
   lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
   ```

6. **List a specific device**

   ```bash
   lsblk /dev/sda
   ```

7. **Show permissions and ownership**

   ```bash
   lsblk -o NAME,MAJ:MIN,RM,SIZE,RO,TYPE,MOUNTPOINT,OWNER,GROUP
   ```

8. **Display all devices including empty ones**

   ```bash
   lsblk -a
   ```

9. **List devices in JSON format**

   ```bash
   lsblk -J
   ```

10. **Show only NAME and SIZE in a clean view**

    ```bash
    lsblk -o NAME,SIZE
    ```
</details>

