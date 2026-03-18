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
