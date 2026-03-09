## 1. `lscpu`

Shows detailed information about the CPU architecture, cores, threads, and processor features.

Examples:

```
lscpu
lscpu | grep MHz
lscpu --extended
```

---

## 2. `cat /proc/cpuinfo`

Displays detailed per-CPU information such as model, cores, cache size, and flags.

Examples:

```
cat /proc/cpuinfo
cat /proc/cpuinfo | grep "model name"
cat /proc/cpuinfo | grep processor
```

---

## 3. `top`

Shows real-time system processes with CPU, memory, and load usage.

Examples:

```
top
top -u root
top -o %MEM
```

---

## 4. `htop`

Interactive process viewer with color display and easier navigation compared to top.

Examples:

```
htop
htop -u user1
htop -d 10
```

---

## 5. `free -h`

Displays system memory usage (RAM and swap) in human-readable format.

Examples:

```
free -h
free -m
free -g
```

---

## 6. `cat /proc/meminfo`

Shows detailed memory statistics of the Linux kernel.

Examples:

```
cat /proc/meminfo
cat /proc/meminfo | grep MemTotal
cat /proc/meminfo | grep Swap
```

---

## 7. `vmstat`

Reports system performance statistics including memory, processes, paging, and CPU activity.

Examples:

```
vmstat
vmstat 5
vmstat 1 10
```

---

## 8. `lsblk`

Lists block devices like disks and partitions in tree format.

Examples:

```
lsblk
lsblk -f
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT
```

---

## 9. `fdisk -l`

Lists disk partitions and details of storage devices.

Examples:

```
fdisk -l
sudo fdisk -l /dev/sda
sudo fdisk -l /dev/nvme0n1
```

---

## 10. `df -h`

Shows disk space usage of mounted filesystems in human-readable format.

Examples:

```
df -h
df -h /home
df -T
```

---

## 11. `blkid`

Displays block device attributes such as UUID and filesystem type.

Examples:

```
blkid
blkid /dev/sda1
blkid | grep ext4
```

---

## 12. `lspci`

Lists all PCI devices such as network cards, GPUs, and storage controllers.

Examples:

```
lspci
lspci | grep VGA
lspci -v
```

---

## 13. `lsusb`

Lists USB devices connected to the system.

Examples:

```
lsusb
lsusb -v
lsusb | grep Logitech
```

---

## 14. `lshw`

Displays detailed hardware configuration of the system.

Examples:

```
sudo lshw
sudo lshw -short
sudo lshw -class network
```

---

## 15. `hwinfo`

Provides detailed hardware information about all devices.

Examples:

```
hwinfo
hwinfo --cpu
hwinfo --disk
```

---

## 16. `dmidecode`

Reads system hardware information from BIOS/SMBIOS such as motherboard, BIOS, and RAM.

Examples:

```
sudo dmidecode
sudo dmidecode -t memory
sudo dmidecode -t system
```

---

## 17. `hostnamectl`

Shows or changes system hostname and system information.

Examples:

```
hostnamectl
hostnamectl set-hostname server01
hostnamectl status
```

---

## 18. `uname -r`

Displays the current Linux kernel version.

Examples:

```
uname -r
uname -r | cut -d- -f1
uname -r | awk -F. '{print $1}'
```

---

## 19. `uname -a`

Displays complete system information including kernel, hostname, architecture, and OS.

Examples:

```
uname -a
uname -a | grep Linux
uname -a | awk '{print $3}'
```

---

## 20. `lsmod`

Lists all currently loaded kernel modules.

Examples:

```
lsmod
lsmod | grep usb
lsmod | wc -l
```

---

## 21. `modprobe`

Loads a kernel module along with its dependencies.

Examples:

```
sudo modprobe vfat
sudo modprobe loop
sudo modprobe nf_conntrack
```

---

## 22. `modprobe -r`

Removes a loaded kernel module.

Examples:

```
sudo modprobe -r vfat
sudo modprobe -r loop
sudo modprobe -r nf_conntrack
```

---

## 23. `insmod`

Inserts a kernel module manually from a specified file.

Examples:

```
sudo insmod module.ko
sudo insmod /lib/modules/module.ko
sudo insmod mydriver.ko
```

---

## 24. `rmmod`

Removes a loaded kernel module from the system.

Examples:

```
sudo rmmod vfat
sudo rmmod loop
sudo rmmod mydriver
```

---

## 25. `dmesg`

Displays kernel ring buffer messages such as boot logs and hardware events.

Examples:

```
dmesg
dmesg | tail
dmesg | grep usb
```

---

## 26. `dmesg | less`

Views kernel messages page-by-page for easier reading.

Examples:

```
dmesg | less
dmesg | less -N
dmesg | less +G
```

---

## 27. `sysctl -a`

Shows all kernel parameters and their current values.

Examples:

```
sysctl -a
sysctl -a | grep net
sysctl -a | grep memory
```

---

## 28. `sysctl`

Displays or retrieves kernel parameter values.

Examples:

```
sysctl kernel.hostname
sysctl vm.swappiness
sysctl net.ipv4.ip_forward
```

---

## 29. `sysctl -w`

Modifies kernel parameters at runtime.

Examples:

```
sudo sysctl -w net.ipv4.ip_forward=1
sudo sysctl -w vm.swappiness=10
sudo sysctl -w kernel.hostname=testserver
```

---

## 30. `cat /proc/version`

Displays Linux kernel version along with compiler and build information.

Examples:

```
cat /proc/version
cat /proc/version | awk '{print $3}'
cat /proc/version | grep gcc
```

---

## 31. `cat /proc/modules`

Shows all currently loaded kernel modules with their usage information.

Examples:

```
cat /proc/modules
cat /proc/modules | grep usb
cat /proc/modules | wc -l
```

---

## 32. `cat /proc/interrupts`

Displays interrupt request (IRQ) usage by devices and CPUs.

Examples:

```
cat /proc/interrupts
cat /proc/interrupts | grep eth
cat /proc/interrupts | grep CPU
```
