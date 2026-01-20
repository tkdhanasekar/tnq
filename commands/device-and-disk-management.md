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
<details>
 <summary>badblocks</summary>

`badblocks` checks a disk or partition for bad (unreadable or unreliable) blocks and reports their block numbers.

1. **Read-only scan of a disk**

   ```bash
   sudo badblocks -sv /dev/sda
   ```

   Scans the entire disk without modifying data.

2. **Read-only scan of a partition**

   ```bash
   sudo badblocks -sv /dev/sda1
   ```

   Checks only the specified partition.

3. **Non-destructive read-write test**

   ```bash
   sudo badblocks -nsv /dev/sda
   ```

   Tests blocks by writing patterns and restoring original data.

4. **Destructive write test**

   ```bash
   sudo badblocks -wsv /dev/sda
   ```

   Overwrites all data to thoroughly test for bad blocks.

5. **Specify block size**

   ```bash
   sudo badblocks -sv -b 4096 /dev/sda
   ```

   Uses a 4 KB block size during testing.

6. **Test a specific block range**

   ```bash
   sudo badblocks -sv 0 500000 /dev/sda
   ```

   Tests only blocks 0 through 500,000.

7. **Save bad blocks to a file**

   ```bash
   sudo badblocks -sv /dev/sda > badblocks.txt
   ```

   Writes the list of bad blocks to a file.

8. **Use bad block list with fsck**

   ```bash
   sudo fsck.ext4 -l badblocks.txt /dev/sda1
   ```

   Marks bad blocks so the filesystem avoids them.

9. **Check during filesystem creation**

   ```bash
   sudo mkfs.ext4 -c /dev/sda1
   ```

   Runs `badblocks` automatically while creating the filesystem.

10. **Force destructive test**

    ```bash
    sudo badblocks -wsvf /dev/sda
    ```

    Forces a destructive test even if safety checks warn you.
</details>
<details>
 <summary>blkid</summary>

`blkid` displays information about block devices, such as filesystem type, UUID, and labels.

1. **List all block devices**

   ```bash
   blkid
   ```

   Shows detected block devices with filesystem details.

2. **Show information for a specific device**

   ```bash
   blkid /dev/sda1
   ```

   Displays UUID, type, and label for the given partition.

3. **Display only the UUID**

   ```bash
   blkid -s UUID /dev/sda1
   ```

   Prints only the UUID field.

4. **Display only the filesystem type**

   ```bash
   blkid -s TYPE /dev/sda1
   ```

   Shows the filesystem type (e.g., ext4, xfs).

5. **Display multiple specific fields**

   ```bash
   blkid -s UUID -s LABEL /dev/sda1
   ```

   Prints only the UUID and label.

6. **Suppress device names**

   ```bash
   blkid -o value -s UUID /dev/sda1
   ```

   Outputs only the UUID value without extra text.

7. **List devices in a specific format**

   ```bash
   blkid -o list
   ```

   Displays block devices in a human-readable table.

8. **Read from a specific block device cache**

   ```bash
   blkid -c /dev/null
   ```

   Forces a fresh scan instead of using the cache.

9. **Show partition table type**

   ```bash
   blkid -s PTTYPE /dev/sda
   ```

   Displays the partition table type (e.g., gpt, dos).

10. **Match a device by UUID**

    ```bash
    blkid -U 123e4567-e89b-12d3-a456-426614174000
    ```

    Finds the device node associated with the given UUID.
</details>
<details>
 <summary>blkdeactivate</summary>

`blkdeactivate` safely deactivates block devices by unmounting filesystems and disabling related device mappings such as LVM and device-mapper targets.

1. **Deactivate all supported block devices**

   ```bash
   sudo blkdeactivate
   ```

   Unmounts and deactivates all detected block devices.

2. **Deactivate a specific device**

   ```bash
   sudo blkdeactivate /dev/sda1
   ```

   Safely unmounts and deactivates the given partition.

3. **Deactivate multiple devices**

   ```bash
   sudo blkdeactivate /dev/sda1 /dev/sdb1
   ```

   Deactivates more than one block device in a single command.

4. **Dry run (show what would be done)**

   ```bash
   sudo blkdeactivate -n
   ```

   Displays actions without making any changes.

5. **Verbose output**

   ```bash
   sudo blkdeactivate -v
   ```

   Shows detailed information about each deactivation step.

6. **Ignore errors and continue**

   ```bash
   sudo blkdeactivate -e
   ```

   Continues processing even if some devices fail to deactivate.

7. **Deactivate only device-mapper devices**

   ```bash
   sudo blkdeactivate -d
   ```

   Limits deactivation to device-mapper (dm) devices.

8. **Deactivate only LVM logical volumes**

   ```bash
   sudo blkdeactivate -l
   ```

   Targets LVM logical volumes specifically.

9. **Combine verbose and dry-run modes**

   ```bash
   sudo blkdeactivate -vn /dev/sda1
   ```

   Shows detailed output of what would happen for a specific device.

10. **Use during shutdown or rescue mode**

    ```bash
    sudo blkdeactivate -v
    ```

    Commonly used in rescue or shutdown scripts to safely release storage.
<details>
 <summary>cfdisk</summary>

`cfdisk` is an interactive, text-based partitioning tool used to create, delete, and modify disk partitions.

1. **Open interactive partition editor for a disk**

   ```bash
   sudo cfdisk /dev/sda
   ```

   Launches the interactive menu for managing partitions on `/dev/sda`.

2. **Use GPT partition table**

   ```bash
   sudo cfdisk -z /dev/sda
   ```

   Creates a new GPT partition table, destroying existing partition data.

3. **Use DOS/MBR partition table**

   ```bash
   sudo cfdisk -z -t dos /dev/sda
   ```

   Creates a new DOS (MBR) partition table.

4. **Display size in sectors**

   ```bash
   sudo cfdisk -u sectors /dev/sda
   ```

   Shows partition sizes in sectors instead of cylinders.

5. **Display size in bytes**

   ```bash
   sudo cfdisk -u bytes /dev/sda
   ```

   Displays partition sizes in bytes.

6. **List supported partition table types**

   ```bash
   cfdisk --list-types
   ```

   Shows all partition table types supported by `cfdisk`.

7. **Force opening even if disk appears in use**

   ```bash
   sudo cfdisk -f /dev/sda
   ```

   Forces access to the disk (use with caution).

8. **Open a different block device**

   ```bash
   sudo cfdisk /dev/nvme0n1
   ```

   Edits partitions on an NVMe disk.

9. **Use cfdisk in rescue or live environment**

   ```bash
   sudo cfdisk /dev/sdb
   ```

   Commonly used to repair or recreate partition layouts.

10. **Exit without writing changes**

    ```bash
    sudo cfdisk /dev/sda
    ```

    Allows reviewing partitions and quitting without saving changes.
</details>
<details>
 <summary>dumpe2fs</summary>

`dumpe2fs` displays detailed metadata and status information of ext2/ext3/ext4 filesystems.

1. **Display full filesystem information**

   ```bash
   sudo dumpe2fs /dev/sda1
   ```

   Shows complete superblock and group descriptor details.

2. **Display only superblock information**

   ```bash
   sudo dumpe2fs -h /dev/sda1
   ```

   Prints a summarized header without block group details.

3. **View filesystem features**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Filesystem features'
   ```

   Lists enabled ext filesystem features.

4. **Check last mount time**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Last mount time'
   ```

   Displays when the filesystem was last mounted.

5. **Check last filesystem check**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Last checked'
   ```

   Shows the last `fsck` execution time.

6. **Display block size**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Block size'
   ```

   Prints the filesystem block size.

7. **View inode count**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Inode count'
   ```

   Displays the total number of inodes.

8. **Display reserved block count**

   ```bash
   sudo dumpe2fs -h /dev/sda1 | grep 'Reserved block count'
   ```

   Shows blocks reserved for the root user.

9. **Find backup superblock locations**

   ```bash
   sudo dumpe2fs /dev/sda1 | grep -i superblock
   ```

   Lists primary and backup superblock block numbers.

10. **Check filesystem state**

    ```bash
    sudo dumpe2fs -h /dev/sda1 | grep 'Filesystem state'
    ```

    Displays whether the filesystem is clean or needs checking.
</details>
<details>
 <summary>delpart</summary>

`delpart` removes a specified partition entry from a block device’s partition table.

1. **Delete a partition**

   ```bash
   sudo delpart /dev/sda 1
   ```

   Removes partition number 1 from disk `/dev/sda`.

2. **Delete a partition on an NVMe disk**

   ```bash
   sudo delpart /dev/nvme0n1 2
   ```

   Deletes partition 2 from an NVMe device.

3. **Delete a partition on a loop device**

   ```bash
   sudo delpart /dev/loop0 1
   ```

   Removes partition 1 from a loopback device.

4. **Delete a partition on a USB drive**

   ```bash
   sudo delpart /dev/sdb 1
   ```

   Deletes the first partition on a USB disk.

5. **Remove a partition before resizing**

   ```bash
   sudo delpart /dev/sda 3
   ```

   Deletes partition 3 so the disk layout can be modified.

6. **Delete a partition used by LVM (after deactivation)**

   ```bash
   sudo delpart /dev/sda 2
   ```

   Removes an LVM-backed partition after logical volumes are disabled.

7. **Delete a partition after unmounting**

   ```bash
   sudo umount /dev/sda1 && sudo delpart /dev/sda 1
   ```

   Unmounts the partition and then removes it from the partition table.

8. **Delete multiple partitions sequentially**

   ```bash
   sudo delpart /dev/sda 1 && sudo delpart /dev/sda 2
   ```

   Removes two partitions one after another.

9. **Remove a partition in a recovery environment**

   ```bash
   sudo delpart /dev/sdc 1
   ```

   Commonly used in rescue or live systems.

10. **Verify partition removal**

    ```bash
    sudo delpart /dev/sda 1 && lsblk
    ```

    Deletes the partition and lists block devices to confirm.
</details>
<details>
 <summary>e2fsck</summary>

`e2fsck` checks and repairs ext2/ext3/ext4 filesystems for inconsistencies and errors.

1. **Check a filesystem**

   ```bash
   sudo e2fsck /dev/sda1
   ```

   Performs a filesystem consistency check on the partition.

2. **Force a full check**

   ```bash
   sudo e2fsck -f /dev/sda1
   ```

   Forces a check even if the filesystem appears clean.

3. **Automatically fix errors**

   ```bash
   sudo e2fsck -y /dev/sda1
   ```

   Answers “yes” to all repair prompts.

4. **Check filesystem without making changes**

   ```bash
   sudo e2fsck -n /dev/sda1
   ```

   Performs a read-only check without modifying data.

5. **Display progress bar**

   ```bash
   sudo e2fsck -C 0 /dev/sda1
   ```

   Shows a progress indicator during the check.

6. **Check and report bad blocks**

   ```bash
   sudo e2fsck -c /dev/sda1
   ```

   Scans for bad blocks using a read-only test.

7. **Use non-destructive read-write bad block test**

   ```bash
   sudo e2fsck -cc /dev/sda1
   ```

   Performs a more thorough bad block scan.

8. **Automatically repair and show progress**

   ```bash
   sudo e2fsck -fy -C 0 /dev/sda1
   ```

   Forces a check, fixes errors, and displays progress.

9. **Check filesystem using an alternate superblock**

   ```bash
   sudo e2fsck -b 32768 /dev/sda1
   ```

   Uses a backup superblock for recovery.

10. **Check filesystem in verbose mode**

    ```bash
    sudo e2fsck -v /dev/sda1
    ```

    Displays detailed information during the check.
</details>
<details>
 <summary>e2label</summary>

`e2label` sets or displays the filesystem label of ext2/ext3/ext4 filesystems.

1. **Display the current filesystem label**

   ```bash
   sudo e2label /dev/sda1
   ```

   Shows the existing label of the filesystem.

2. **Set a new filesystem label**

   ```bash
   sudo e2label /dev/sda1 DATA
   ```

   Assigns the label `DATA` to the filesystem.

3. **Clear the filesystem label**

   ```bash
   sudo e2label /dev/sda1 ""
   ```

   Removes any existing label.

4. **Change label on an unmounted filesystem**

   ```bash
   sudo umount /dev/sda1 && sudo e2label /dev/sda1 BACKUP
   ```

   Safely updates the label after unmounting.

5. **Verify the new label**

   ```bash
   sudo e2label /dev/sda1
   ```

   Confirms the label change.

6. **Set label during filesystem creation**

   ```bash
   sudo mkfs.ext4 -L HOME /dev/sda1
   ```

   Creates an ext4 filesystem with the label `HOME`.

7. **List labels using blkid**

   ```bash
   blkid | grep LABEL
   ```

   Displays filesystem labels for all devices.

8. **Use label for mounting**

   ```bash
   sudo mount LABEL=DATA /mnt/data
   ```

   Mounts a filesystem using its label.

9. **Relabel a USB or removable drive**

   ```bash
   sudo e2label /dev/sdb1 USBSTORE
   ```

   Sets a label for a removable ext filesystem.

10. **Check label length limits**

    ```bash
    sudo e2label /dev/sda1 VERYLONGNAME
    ```

    Demonstrates label length limits (typically up to 16 characters).
</details>
<details>
 <summary>fdisk</summary>

`fdisk` is a command-line utility used to view, create, delete, and manage disk partition tables.

1. **List all disks and partitions**

   ```bash
   sudo fdisk -l
   ```

   Displays partition tables for all detected disks.

2. **List partitions on a specific disk**

   ```bash
   sudo fdisk -l /dev/sda
   ```

   Shows partition details for `/dev/sda`.

3. **Open interactive partition editor**

   ```bash
   sudo fdisk /dev/sda
   ```

   Starts interactive mode to manage disk partitions.

4. **Create a new partition table**

   ```bash
   sudo fdisk /dev/sda
   ```

   Allows creating a new DOS or GPT partition table from the menu.

5. **Delete an existing partition**

   ```bash
   sudo fdisk /dev/sda
   ```

   Deletes a partition using the interactive delete option.

6. **Change partition type**

   ```bash
   sudo fdisk /dev/sda
   ```

   Modifies the partition type (for example, Linux, swap).

7. **Write changes to disk**

   ```bash
   sudo fdisk /dev/sda
   ```

   Saves partition changes and updates the disk.

8. **Exit without saving changes**

   ```bash
   sudo fdisk /dev/sda
   ```

   Quits without writing any changes.

9. **Show disk geometry**

   ```bash
   sudo fdisk -l /dev/sda
   ```

   Displays sector size, disk size, and layout information.

10. **Verify partition table**

    ```bash
    sudo fdisk -v
    ```

    Shows the `fdisk` version to verify tool availability.
</details>
<details>
 <summary>findfs</summary>

`findfs` locates a filesystem by its label or UUID and returns the corresponding device name.

1. **Find device by label**

```bash
sudo findfs LABEL=DATA
```

Returns the device corresponding to the filesystem labeled `DATA`.

2. **Find device by UUID**

```bash
sudo findfs UUID=123e4567-e89b-12d3-a456-426614174000
```

Locates the device using the filesystem UUID.

3. **Use in a mount command by label**

```bash
sudo mount $(findfs LABEL=DATA) /mnt/data
```

Finds the device by label and mounts it.

4. **Use in a mount command by UUID**

```bash
sudo mount $(findfs UUID=123e4567-e89b-12d3-a456-426614174000) /mnt/backup
```

Finds the device by UUID and mounts it to a directory.

5. **List all devices with a specific label**

```bash
sudo findfs LABEL=USB_DRIVE
```

Outputs the device node for a USB drive with the given label.

6. **Use with scripts for dynamic mounting**

```bash
DEVICE=$(findfs LABEL=DATA); sudo mount $DEVICE /mnt/data
```

Stores the device in a variable for automated scripts.

7. **Verify a filesystem exists by UUID**

```bash
findfs UUID=123e4567-e89b-12d3-a456-426614174000
```

Returns the device if it exists, empty if not.

8. **Check removable media**

```bash
findfs LABEL=MY_USB
```

Finds a USB drive by its label.

9. **Use with `blkid` for confirmation**

```bash
sudo blkid $(findfs LABEL=DATA)
```

Displays filesystem details of the device found by label.

10. **Combine with `fsck` for maintenance**

```bash
sudo fsck $(findfs LABEL=DATA)
```

Checks and repairs the filesystem located by its label.
</details>
<details>
 <summary>findmnt</summary>

`findmnt` displays mounted filesystems, their mount points, source devices, and related information.

1. **Show all mounted filesystems**

```bash
findmnt
```

Displays a tree of all currently mounted filesystems.

2. **Show a specific mount point**

```bash
findmnt /mnt/data
```

Shows detailed information for the `/mnt/data` mount point.

3. **Show filesystem type only**

```bash
findmnt -t ext4
```

Lists all mounted ext4 filesystems.

4. **Show devices with a specific label**

```bash
findmnt -L DATA
```

Finds the mount point of the filesystem labeled `DATA`.

5. **Show devices with a specific UUID**

```bash
findmnt -U 123e4567-e89b-12d3-a456-426614174000
```

Displays the mount point of the filesystem with the given UUID.

6. **Output in list format**

```bash
findmnt -l
```

Displays mounted filesystems in a simple list format rather than a tree.

7. **Show only source devices**

```bash
findmnt -o SOURCE
```

Lists only the device names of mounted filesystems.

8. **Show mount points and options**

```bash
findmnt -o TARGET,OPTIONS
```

Displays the mount points along with their mount options.

9. **Show all filesystems including unmounted**

```bash
findmnt -a
```

Lists all available filesystems, mounted or not.

10. **Filter by filesystem type and display tree**

```bash
findmnt -t xfs
```

Shows only mounted XFS filesystems in a tree format.
</details>
<details>
 <summary>fsck</summary>

`fsck` (filesystem check) checks and repairs Linux filesystems for errors and inconsistencies.

1. **Check a filesystem**

```bash
sudo fsck /dev/sda1
```

Performs a basic filesystem check on the partition `/dev/sda1`.

2. **Automatically repair errors**

```bash
sudo fsck -y /dev/sda1
```

Answers “yes” to all prompts and fixes errors automatically.

3. **Force a check even if filesystem is clean**

```bash
sudo fsck -f /dev/sda1
```

Forces a full check even if the filesystem appears healthy.

4. **Check without making changes**

```bash
sudo fsck -n /dev/sda1
```

Performs a read-only check without modifying the filesystem.

5. **Check all filesystems listed in /etc/fstab**

```bash
sudo fsck -A
```

Runs a check on all filesystems defined in `/etc/fstab`.

6. **Check filesystems in parallel**

```bash
sudo fsck -A -T
```

Checks all filesystems in `/etc/fstab` without showing the title for each.

7. **Interactive repair with verbose output**

```bash
sudo fsck -v /dev/sda1
```

Displays detailed information and prompts before repairs.

8. **Limit check to a specific filesystem type**

```bash
sudo fsck -t ext4 /dev/sda1
```

Checks only ext4 filesystems and skips others.

9. **Use alternate superblock for recovery**

```bash
sudo fsck -b 32768 /dev/sda1
```

Uses a backup superblock to recover a corrupted filesystem.

10. **Skip mounted filesystems**

```bash
sudo fsck -M /dev/sda1
```

Prevents checking filesystems that are currently mounted.
</details>
<details>
 <summary>fsck.ext4</summary>


`fsck.ext4` checks and repairs ext4 filesystems, similar to `fsck` but specific to ext4.

1. **Check an ext4 filesystem**

```bash
sudo fsck.ext4 /dev/sda1
```

Performs a basic consistency check on `/dev/sda1`.

2. **Automatically repair errors**

```bash
sudo fsck.ext4 -y /dev/sda1
```

Fixes all detected errors without prompting.

3. **Force a check even if clean**

```bash
sudo fsck.ext4 -f /dev/sda1
```

Forces a full check regardless of filesystem state.

4. **Perform read-only check**

```bash
sudo fsck.ext4 -n /dev/sda1
```

Checks for errors without modifying the filesystem.

5. **Check and show progress**

```bash
sudo fsck.ext4 -C 0 /dev/sda1
```

Displays a progress bar during the check.

6. **Use alternate superblock**

```bash
sudo fsck.ext4 -b 32768 /dev/sda1
```

Uses a backup superblock for recovery if the primary is corrupted.

7. **Verbose output**

```bash
sudo fsck.ext4 -v /dev/sda1
```

Displays detailed information about the check and repairs.

8. **Check for bad blocks (read-only)**

```bash
sudo fsck.ext4 -c /dev/sda1
```

Scans for bad blocks without writing to them.

9. **Check for bad blocks (non-destructive read-write)**

```bash
sudo fsck.ext4 -cc /dev/sda1
```

Performs a more thorough scan of bad blocks, preserving data.

10. **Skip mounted filesystem**

```bash
sudo fsck.ext4 -M /dev/sda1
```

Prevents checking the filesystem if it is currently mounted.
</details>
<details>
 <summary>hdparm</summary>

`hdparm` is a command-line utility for viewing and tuning hard disk parameters, including performance and power management.

1. **View basic drive information**

```bash
sudo hdparm -I /dev/sda
```

Displays detailed information about the disk, including model, firmware, and capabilities.

2. **Show current drive settings**

```bash
sudo hdparm -i /dev/sda
```

Displays essential identification and current parameters.

3. **Measure read speed (benchmark)**

```bash
sudo hdparm -t /dev/sda
```

Performs a read-only speed test of the drive.

4. **Measure cached read speed**

```bash
sudo hdparm -T /dev/sda
```

Tests the read speed from the drive cache.

5. **Enable write caching**

```bash
sudo hdparm -W1 /dev/sda
```

Turns on the drive’s write cache for improved performance.

6. **Disable write caching**

```bash
sudo hdparm -W0 /dev/sda
```

Disables the write cache for safer writes at the cost of speed.

7. **Set power-down (sleep) timeout**

```bash
sudo hdparm -S 120 /dev/sda
```

Sets the drive to spin down after 10 minutes of inactivity (120 × 5 seconds).

8. **Enable DMA (Direct Memory Access)**

```bash
sudo hdparm -d1 /dev/sda
```

Activates DMA mode for faster data transfers.

9. **Set drive acoustic management (reduce noise)**

```bash
sudo hdparm -M 128 /dev/sda
```

Adjusts the drive for quieter operation; lower values are quieter.

10. **Securely erase a drive**

```bash
sudo hdparm --security-erase NULL /dev/sda
```

Performs a secure erase, wiping all data (use with caution).
</details>
<details>
 <summary>lsblk</summary>

`lsblk` lists information about all available block devices in a tree-like format, showing partitions, sizes, and mount points.

1. **List all block devices**

```bash
lsblk
```

Shows all disks and partitions in a tree format.

2. **List devices with filesystem type**

```bash
lsblk -f
```

Displays filesystem type, label, UUID, and mount points.

3. **List devices with sizes**

```bash
lsblk -o NAME,SIZE
```

Shows only the device name and size.

4. **Show all details including partitions and devices**

```bash
lsblk -a
```

Lists all devices, including empty or unpartitioned ones.

5. **Show mount points**

```bash
lsblk -o NAME,MOUNTPOINT
```

Displays each device and where it is mounted.

6. **List devices in JSON format**

```bash
lsblk -J
```

Outputs block device information as JSON for scripting.

7. **List devices in list format (no tree)**

```bash
lsblk -l
```

Shows all devices in a flat list format instead of a tree.

8. **Include filesystem UUIDs and labels**

```bash
lsblk -o NAME,FSTYPE,LABEL,UUID
```

Displays devices along with filesystem type, label, and UUID.

9. **Show only disks (exclude partitions)**

```bash
lsblk -d
```

Lists only the top-level disks, not their partitions.

10. **Filter by a specific device**

```bash
lsblk /dev/sda
```

Displays information only for `/dev/sda` and its partitions.
</details>
<details>
