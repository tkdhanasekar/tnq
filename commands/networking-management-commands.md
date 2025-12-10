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
</summary>
  

