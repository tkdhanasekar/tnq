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
