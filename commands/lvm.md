**LVM (Logical Volume Manager)** is a storage management system in Linux that allows you to manage disk space more flexibly than traditional partitioning. Instead of fixed disk partitions, LVM lets you create **logical volumes** that can be resized, extended, or moved easily across physical storage devices.

### Key Concepts (quickly)

* **Physical Volume (PV):** Actual disk or partition
* **Volume Group (VG):** Pool of storage created from one or more PVs
* **Logical Volume (LV):** Virtual partition created from a VG (used like a normal disk)

---

## Advantages of LVM

* **Flexible resizing**

  * Easily increase or decrease the size of logical volumes without major downtime

* **Storage pooling**

  * Combine multiple disks into a single volume group for better space utilization

* **Easy disk management**

  * Add or remove disks without disrupting the system significantly

* **Snapshots**

  * Create backups of the system at a point in time (useful for backups and testing)

* **Better utilization of space**

  * Allocate space dynamically instead of fixed partitions

* **Online resizing**

  * Extend volumes while the system is running (in many cases)

* **Data migration**

  * Move data between physical disks without unmounting (using tools like `pvmove`)

* **RAID support (via LVM or integration)**

  * Supports striping, mirroring, etc. for performance and redundancy
  
---

## LVM commands list
```
config
devtypes
dumpconfig
formats
fullreport
help
lastlog
lvchange
lvconvert
lvcreate
lvdisplay
lvextend
lvmchange
lvmconfig
lvmdevices
lvmdiskscan
lvmsadc
lvmsar
lvpoll
lvreduce
lvremove
lvrename
lvresize
lvs
lvscan
pvchange
pvck
pvcreate
pvdata
pvdisplay
pvmove
pvremove
pvresize
pvs
pvscan
segtypes
systemid
tags
version
vgcfgbackup
vgcfgrestore
vgchange
vgck
vgconvert
vgcreate
vgdisplay
vgexport
vgextend
vgimport
vgimportclone
vgimportdevices
vgmerge
vgmknodes
vgreduce
vgremove
vgrename
vgs
vgscan
vgsplit
```

To view the added volumes
```
lsblk
```
To enter into lvm mode
```
lvm
```
To view the available commands
```
> help
```
To create the physical volumes
```
> pvcreate /dev/sdc /dev/sdd /dev/sde
```
To Display information about physical volumes
```
> pvs
```
To create the volume group with /dev/sdc/ /dev/sdd /dev/sde
```
> vgcreate <name_of_volume_group> /dev/sdc /dev/sdd /dev/sde
> vgcreate my_vg /dev/sdc /dev/sdd /dev/sde
```
To Display information about volume groups
```
> vgs
```
To Create a logical volume my_lv of 10GB
```
> lvcreate -L 10G -n my_lv my_vg
```
To Display information about logical volumes
```
> lvs
```
View Attached Storage Devices with lsblk​
```
lsblk
```
Check Disk Space Usage with df -Th
```
df -Th
```
We can't see /dev/sdc /dev/sdd /dev/sde because they are not mounted yet
mounted yet. create mount point
```
mkdir /mnt/my_lv_mount
```
To create a filesystem on the logical volume, we use the mkfs.ext4 command
```
mkfs.ext4 /dev/<VG_NAME>/<LV_NAME>
```
```
mkfs.ext4 /dev/my_vg/my_lv
```
Mount the logical volume
```
mount /dev/my_vg/my_lv /mnt/my_lv_mount
```
now check with df -Th command
```
df -Th
```
navigate to /mnt/my_lv_mount
```
cd /mnt/my_lv_mount
```
create folders and files
```
mkdir test_folder
touch file.txt
```
```
ls
```
To increase the logical volume by 5 GB
```
lvextend -L +5G /dev/vg_name/lv_name
```
```
df -Th
```
it will not show the increased 5GB to fix it
```
resize2fs /dev/my_vg/my_lv
```
now check with
```
df -Th
```
To make lvreduce follow the workflow
```
Correct order for shrinking:
umount
e2fsck
resize2fs
lvreduce
If you did lvreduce first, filesystem may be partially lost.
```
1. **Unmount the filesystem**

```
umount /mnt/my_lv_mount
```

2. **Check filesystem (recommended)**

```
e2fsck -f /dev/my_vg/my_lv
```

3. **Shrink the filesystem first (IMPORTANT)**

```
resize2fs /dev/my_vg/my_lv 10G
```

4. **Then reduce the logical volume**

```
lvreduce -L 10G /dev/my_vg/my_lv
```

5. **Mount back**

```
mount /dev/my_vg/my_lv /mnt/my_lv_mount
```

6. **Verify**

```
df -Th
```

**Key point:**

* Always **shrink filesystem first**, then run `lvreduce`.
* Shrinking cannot be done while mounted.

