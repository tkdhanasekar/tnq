Here are the exact steps to install QEMU + KVM on Ubuntu 24.04 LTS (Noble Numbat) and enable virtualization:

1. Verify hardware virtualization support

Open a terminal and run:
```
LC_ALL=C lscpu | grep Virtualization
```

You should see either:

 Virtualization: VT-x (Intel)
 Virtualization: AMD-V (AMD)

Then check if KVM modules can load:
```
lsmod | grep kvm
```
If empty, that's OK—you’ll load them after installation.

---

2. Install QEMU, KVM, libvirt, and virt-manager

This installs everything needed for virtualization:

```
sudo apt update
```
```
sudo apt install -y qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager ovmf
```

 What these packages are:

| Package                   | Purpose                         |
| ------------------------- | ------------------------------- |
| qemu-kvm              | QEMU with hardware acceleration |
| libvirt-daemon-system | libvirt virtualization service  |
| libvirt-clients       | CLI tools (virsh, virt-install) |
| bridge-utils          | Network bridging                |
| virt-manager          | GUI virtual machine manager     |
| ovmf                  | UEFI firmware for VMs           |

---

3. Add your user to the libvirt group

This allows running VMs without root:

```
sudo usermod -aG libvirt $USER
```
```
sudo usermod -aG kvm $USER
```

Then log out and back in (or reboot).

---

4. Check that KVM is working

Check libvirtd status:

```
systemctl status libvirtd
```

It should show active (running).

 Check if KVM acceleration is available:

```
virt-host-validate
```

Look for:


QEMU: Checking for hardware virtualization: PASS
KVM: /dev/kvm exists: PASS


---

5. Launch virt-manager

Start the GUI:

```
virt-manager
```
```
virsh list --all
```

---

Optional: Enable bridged networking (for VMs with LAN IPs)

If you want VMs to appear directly on your local network:

```
sudo nano /etc/netplan/01-bridge.yaml
```

Example config:
```
yaml
network:
  version: 2
  renderer: NetworkManager
  bridges:
    br0:
      interfaces: [enp3s0]
      dhcp4: true
```

Apply:

```
sudo netplan apply
```

---
