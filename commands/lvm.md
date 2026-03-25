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
## To increase the logical volume by 5 GB
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
## To make lvreduce follow the workflow
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

## examples:

**config** – Displays LVM configuration settings  
`lvm config`

**devtypes** – Lists supported device types for LVM  
`lvm devtypes`

**dumpconfig** – Shows full LVM configuration in a readable format  
`lvm dumpconfig`

**formats** – Displays available metadata formats used by LVM  
`lvm formats`

**fullreport** – Generates a comprehensive report of PVs, VGs, and LVs  
`lvm fullreport`

**help** – Provides help information about LVM commands  
`lvm help`

**lastlog** – Shows the last LVM command log (recent LVM operations)  
`lvm lastlog`

**lvchange** – Change attributes of a logical volume (e.g., activate/deactivate).  
`lvchange -ay /dev/my_vg/my_lv`  (activate LV)

**lvconvert** – Convert a logical volume (e.g., to mirror, raid).  
`lvconvert --mirror 1 /dev/my_vg/my_lv`  (convert LV to mirrored)

**lvcreate** – Create a new logical volume.  
`lvcreate -n my_lv -L 10G my_vg`  (create 10G LV in my_vg)

**lvdisplay** – Show detailed info about logical volumes.  
`lvdisplay`

**lvextend** – Increase the size of a logical volume.  
`lvextend -L +5G /dev/my_vg/my_lv`  (increase LV by 5G)

**lvmchange** – Modify LVM configuration or attributes (rarely used).  
`lvmchange --yes`  (apply pending changes interactively)

**lvmconfig** – Display or edit LVM configuration.  
`lvmconfig --type full`  (show full LVM config)

**lvmdevices** – List all detected block devices for LVM.  
`lvmdevices`  (scan /dev/sdc, /dev/sdd)

**lvmdiskscan** – Scan all disks for LVM physical volumes.  
`lvmdiskscan`

**lvmsadc** – Collect LVM statistics for monitoring.  
`lvmsadc --interval 10 --count 6`  (stats every 10s, 6 times)

**lvmsar** – Display LVM statistics in sar format.  
`lvmsar`  (report LV statistics)

**lvpoll** – Poll LVM devices for changes.  
`lvpoll`  (update LVM metadata if devices changed)

**lvreduce** – Reduce size of a logical volume (dangerous, data loss risk).  
`lvreduce -L 5G /dev/my_vg/my_lv`  (shrink LV to 5G)

**lvremove** – Remove a logical volume.  
`lvremove /dev/my_vg/my_lv`  (delete LV)

**lvrename** – Rename a logical volume.  
`lvrename my_vg my_lv my_lv_new`

**lvresize** – Resize a logical volume (extend or reduce).  
`lvresize -L 15G /dev/my_vg/my_lv`  (resize LV to 15G)

**lvs** – List logical volumes in a summary form.  
`lvs`  (show all LVs)

**lvscan** – Scan all LVs on the system.  
`lvscan`  (display all detected LVs)

**pvchange** – Change attributes of a physical volume.  
`pvchange -ay /dev/sdc`  (activate PV)

**pvck** – Check a physical volume for consistency.  
`pvck /dev/sdc`

**pvcreate** – Initialize a block device as a physical volume for LVM.  
`pvcreate /dev/sdc /dev/sdd`

**pvdata** – Display detailed metadata of a physical volume.  
`pvdata /dev/sdc`

**pvdisplay** – Show detailed information about a physical volume.  
`pvdisplay /dev/sdc`

**pvmove** – Move data from one physical volume to another within a VG.  
`pvmove /dev/sdc /dev/sdd`

**pvremove** – Remove LVM metadata from a physical volume.  
`pvremove /dev/sdc`

**pvresize** – Resize a physical volume to use added space.  
`pvresize /dev/sdc`

**pvs** – List all physical volumes in a summary table.  
`pvs`

**pvscan** – Scan all disks for LVM physical volumes.  
`pvscan`

**segtypes** – List supported LVM segment types (linear, striped, mirrored, etc.).  
`segtypes`

**systemid** – Show the system ID for a device (used for LVM/metadata identification).  
`systemid /dev/sdc`

**tags** – Display or assign tags to LVM objects (LV, VG, or PV) for filtering.  
`tags /dev/my_vg/my_lv`

**version** – Show the installed LVM version.  
`version`

**vgcfgbackup** – Backup the metadata of a volume group.  
`vgcfgbackup my_vg`

**vgcfgrestore** – Restore volume group metadata from a backup.  
`vgcfgrestore my_vg`

**vgchange** – Change attributes of a volume group (activate/deactivate).  
`vgchange -ay my_vg`

**vgck** – Check volume group metadata for consistency.  
`vgck my_vg`

**vgconvert** – Convert a volume group to a different format (e.g., clustered).  
`vgconvert --clustered y my_vg`

**vgcreate** – Create a new volume group using physical volumes.  
`vgcreate my_vg /dev/sdc /dev/sdd`

**vgdisplay** – Show detailed information about a volume group.  
`vgdisplay my_vg`

**vgexport** – Mark a volume group as exportable for moving to another system.  
`vgexport my_vg`

**vgextend** – Add physical volumes to an existing volume group.  
`vgextend my_vg /dev/sdd`

**vgimport** – Import an exported volume group into the system.  
Example: `vgimport my_vg`

**vgimportclone** – Import a cloned VG with a new identifier.  
`vgimportclone my_vg`

**vgimportdevices** – Import volume groups detected on local devices.  
`vgimportdevices`

**vgmerge** – Merge two volume groups into one.  
`vgmerge my_vg my_vg2`

**vgmknodes** – Create device nodes for all logical volumes in a VG.  
`vgmknodes my_vg`

**vgreduce** – Remove physical volumes from a volume group.  
`vgreduce my_vg /dev/sdd`

**vgremove** – Remove a volume group (after removing all LVs).  
`vgremove my_vg`

**vgrename** – Rename a volume group.  
`vgrename my_vg my_vg_new`

**vgs** – List volume groups in a summary table.  
`vgs`

**vgscan** – Scan all disks for volume groups.  
`vgscan`

**vgsplit** – Split a volume group into two separate VGs.  
`vgsplit my_vg my_vg_new /dev/sdd`
