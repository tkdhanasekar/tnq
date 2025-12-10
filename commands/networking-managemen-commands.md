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

