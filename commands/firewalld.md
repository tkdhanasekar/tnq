# firewalld 

## Service Control

```bash
sudo apt install firewalld
systemctl start firewalld
systemctl stop firewalld
systemctl restart firewalld
systemctl enable firewalld
systemctl disable firewalld
systemctl status firewalld
```

---

## Check Status

```bash
firewall-cmd --state
firewall-cmd --list-all
firewall-cmd --list-services
firewall-cmd --list-ports
```

---

## Zones

```bash
firewall-cmd --get-zones
firewall-cmd --get-default-zone
firewall-cmd --set-default-zone=public

firewall-cmd --get-active-zones
```

Assign interface to zone:

```bash
firewall-cmd --zone=public --add-interface=eth0
```

---

## Open / Close Ports

### Open port (temporary)

```bash
firewall-cmd --add-port=8080/tcp
```

### Open port (permanent)

```bash
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --reload
```

### Remove port

```bash
firewall-cmd --permanent --remove-port=8080/tcp
firewall-cmd --reload
```

---

## Allow / Remove Services

### Allow service

```bash
firewall-cmd --add-service=http
firewall-cmd --permanent --add-service=https
firewall-cmd --reload
```

### Remove service

```bash
firewall-cmd --permanent --remove-service=http
firewall-cmd --reload
```

---

## Rich Rules (Advanced)

Allow IP:

```bash
firewall-cmd --permanent \
  --add-rich-rule='rule family="ipv4" source address="192.168.1.100" accept'
```

Block IP:

```bash
firewall-cmd --permanent \
  --add-rich-rule='rule family="ipv4" source address="192.168.1.100" reject'
```

Reload:

```bash
firewall-cmd --reload
```

---

## Masquerading (NAT)

```bash
firewall-cmd --add-masquerade
firewall-cmd --permanent --add-masquerade
firewall-cmd --reload
```

---

## Port Forwarding

```bash
firewall-cmd --permanent \
  --add-forward-port=port=80:proto=tcp:toport=8080

firewall-cmd --reload
```

Forward to another IP:

```bash
firewall-cmd --permanent \
  --add-forward-port=port=80:proto=tcp:toaddr=192.168.1.10:toport=8080
```

---

## Reload & Runtime vs Permanent

Reload rules:

```bash
firewall-cmd --reload
```

Runtime vs permanent:

* Runtime = immediate, lost after reboot
* Permanent = saved, needs reload

Copy runtime → permanent:

```bash
firewall-cmd --runtime-to-permanent
```

---

## Direct Rules (Low-level)

```bash
firewall-cmd --direct --add-rule ipv4 filter INPUT 0 -p tcp --dport 22 -j ACCEPT
```

---

## Panic Mode (Emergency Lockdown)

```bash
firewall-cmd --panic-on
firewall-cmd --panic-off
```

---

## Useful Combos

Open HTTP + HTTPS permanently:

```bash
firewall-cmd --permanent --add-service={http,https}
firewall-cmd --reload
```

Quick debug:

```bash
firewall-cmd --list-all --zone=public
```

---

## Tips

* Always use `--permanent` + `--reload` for lasting changes
* Use zones to segment trust levels (public, internal, dmz)
* Prefer **services** over raw ports when possible

---

## Port Forwarding

Firewalld port forwarding is a feature in Linux that allows network traffic arriving at one port or interface on your system to be automatically redirected to another port or another host. It's commonly used for services running behind a firewall or when you want to expose internal services externally without changing the service configuration.

Here’s a detailed breakdown:

---

### 1. **What Firewalld Is**

**Firewalld** is a dynamic firewall management tool on Linux that uses zones and services to control network traffic. Unlike static iptables rules, firewalld allows you to apply changes without restarting the firewall.

---

### 2. **What Port Forwarding Means**

Port forwarding (also called **DNAT – Destination Network Address Translation**) is when incoming traffic to a specific port is redirected to a different port or IP address. For example:

* Redirect traffic coming to port **8080** on your public IP to port **80** on an internal server.
* Allow external access to an internal service running on a non-public IP.

---

### 3. **Firewalld Port Forwarding Syntax**

Firewalld uses **rich rules** or **direct rules** for port forwarding.

#### Example with Rich Rules:

```bash
firewall-cmd --permanent --zone=public --add-rich-rule='
  rule family="ipv4"
  forward-port port=8080 protocol=tcp to-port=80 to-addr=192.168.1.100'
```

Explanation:

* `zone=public` → The network zone where this rule applies.
* `port=8080` → Incoming port.
* `protocol=tcp` → Protocol (TCP or UDP).
* `to-port=80` → Destination port.
* `to-addr=192.168.1.100` → Destination IP.

After adding a permanent rule, reload firewalld:

```bash
firewall-cmd --reload
```

---

### 4. **Other Key Points**

* Firewalld port forwarding only works if **IP forwarding** is enabled:

```bash
sysctl -w net.ipv4.ip_forward=1
```

To make it permanent:

```bash
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
sysctl -p
```

* You can also specify **protocol**, **zone**, and whether forwarding applies to IPv4 or IPv6.
* Useful for **NAT setups**, **VPNs**, and exposing services behind NAT/firewalls.

---

### 5. **Quick Use Case**

Imagine you have a web server on your private network at **192.168.1.50:80**. Your firewall public IP is **203.0.113.10**, and you want users accessing **203.0.113.10:8080** to reach that web server. Firewalld port forwarding handles this automatically.

---

## Masquerading
Firewalld **Masquerading (NAT)** is a networking feature in Linux that allows a machine to act as a **gateway**, enabling multiple devices on a private network to access external networks (like the Internet) using a single public IP address. Let’s break it down carefully.

---

### 1. **What Masquerading Means**

* Masquerading is a type of **Network Address Translation (NAT)**.
* NAT modifies network packets so that devices in a private network can communicate with external networks.
* **Masquerading specifically** is used when the outgoing IP address of the gateway is **dynamic** (changes over time, e.g., via DHCP).

Essentially, your internal devices’ IP addresses are hidden (“masqueraded”) behind the public IP of the firewall machine.

---

### 2. **How It Works**

1. Device inside the network (e.g., 192.168.1.10) wants to reach the internet.
2. Packet reaches the firewall (running firewalld) with masquerading enabled.
3. Firewalld replaces the **source IP** (192.168.1.10) with the firewall’s public IP (e.g., 203.0.113.5) before sending it out.
4. Response from the internet comes back to the firewall’s public IP.
5. Firewall translates the **destination IP** back to the internal device (192.168.1.10) and forwards it.

This allows multiple internal devices to share a single public IP.

---

### 3. **When You Use It**

* Home or office networks where only one public IP is available.
* Routing traffic from a private subnet to the internet.
* Situations where you don’t want to assign public IPs to every device.

---

### 4. **firewalld Commands for Masquerading**

Firewalld is a dynamic firewall manager in Linux. To enable masquerading:

**Step 1: Check the current zones**

```bash
firewall-cmd --get-active-zones
```

**Step 2: Enable masquerading for a zone (e.g., `public`)**

```bash
firewall-cmd --zone=public --add-masquerade
```

**Step 3: Make it permanent**

```bash
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --reload
```

---

### 5. **Key Points**

* Masquerading is **dynamic NAT**.
* Useful when your **public IP changes**.
* Works well for **outgoing connections** but not for incoming connections unless you configure **port forwarding**.
* Different from **static NAT**, which maps fixed private IPs to fixed public IPs.

---

## Zones

In **firewalld**, **Zones** are essentially **predefined sets of rules that define the level of trust you place in network connections**. They let you control which traffic is allowed or blocked, based on the network you’re connected to. Think of zones as **profiles for your network interfaces**.

Here’s the concept step by step:

---

### 1. **Purpose of Zones**

* Firewalld uses zones to **simplify firewall management**.
* Instead of writing complex iptables rules manually, you assign a network interface or source IP to a zone, and the zone’s rules automatically apply.
* Each zone defines **allowed services, ports, protocols, and source addresses**.

---

### 2. **Common Predefined Zones**

Firewalld comes with several zones, each with a different trust level:

| Zone         | Trust Level | Typical Use Case                                                                           |
| ------------ | ----------- | ------------------------------------------------------------------------------------------ |
| **drop**     | None        | All incoming packets are dropped; no responses sent.                                       |
| **block**    | Low         | All incoming packets are rejected with an ICMP message; only outgoing connections allowed. |
| **public**   | Low         | For use in public places (cafes, airports); only essential services allowed.               |
| **external** | Medium      | For routers/firewalls; masquerading enabled if needed.                                     |
| **dmz**      | Medium      | For publicly accessible servers; limited access.                                           |
| **work**     | Medium      | Trusted work network; more services allowed.                                               |
| **home**     | High        | For home network; most services allowed.                                                   |
| **internal** | High        | For internal networks; more permissive than public.                                        |
| **trusted**  | Full        | All incoming connections are allowed.                                                      |

---

### 3. **How Zones Work**

* You can assign **interfaces** (like `eth0`) or **source IPs** to zones.
* Rules in that zone apply automatically to traffic coming from those sources.
* Example: Your laptop might use `home` when connected to your home Wi-Fi, but `public` when connected to a café’s network.

---

### 4. **Managing Zones**

Some useful `firewalld` commands:

```bash
# List all available zones
firewall-cmd --get-zones

# See which zone is active for an interface
firewall-cmd --get-active-zones

# Assign an interface to a zone
firewall-cmd --zone=home --change-interface=eth0

# Add a service (like HTTP) to a zone
firewall-cmd --zone=public --add-service=http

# Make changes permanent
firewall-cmd --runtime-to-permanent
```

---

### ✅ Summary

* **Zones are profiles for network trust.**
* They make firewall management **easier and safer**.
* Choosing the right zone depends on **where you are and how much trust you have in the network**.
