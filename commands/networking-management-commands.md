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




