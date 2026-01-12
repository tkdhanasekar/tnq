<details>
 <summary>du</summary>

1. **Check disk usage of the current directory**

```
du
```

2. **Show disk usage in human-readable format (KB, MB, GB)**

```
du -h
```

3. **Check disk usage of a specific directory**

```
du -h /var/log
```

4. **Show disk usage of all files and directories (not just directories)**

```
du -ah
```

5. **Display only the total size of a directory**

```
du -sh /home/user
```

6. **Show disk usage for each subdirectory (one level deep)**

```
du -h --max-depth=1 /home
```

7. **Sort directories by size (largest first)**

```
du -h --max-depth=1 | sort -hr
```

8. **Exclude specific directories**

```
du -h --exclude=cache
```

9. **Check disk usage using a specific block size**

```
du -h --block-size=1G
```

10. **Summarize disk usage of multiple directories**

```
du -sh /etc /usr /var
```
11. **To find the top 10 biggest files using du for the entire system**
```
sudo du -ah / | sort -hr | head -n 10
```
</details>
<details>
 <summary>df</summary>
 
1. **Show disk space usage for all mounted filesystems**

```
df
```

2. **Display disk usage in human-readable format (KB, MB, GB)**

```
df -h
```

3. **Show disk usage in human-readable format using powers of 1000**

```
df -H
```

4. **Show disk usage for a specific directory**

```
df /home
```

5. **Show disk usage including filesystem type**

```
df -T
```

6. **Show disk usage for all filesystems, including dummy (pseudo) filesystems**

```
df -a
```

7. **Display disk usage in kilobytes**

```
df -k
```

8. **Display disk usage in megabytes**

```
df -m
```

9. **Exclude specific filesystem types (for example, tmpfs)**

```
df -x tmpfs
```

10. **Display inode usage instead of block usage**

```
df -i
```
</details>
