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
<details>
 <summary>fallocate</summary>

1. **Create a file of a specific size (1 GB)**

```
fallocate -l 1G myfile.img
```

2. **Create a file of 500 MB**

```
fallocate -l 500M datafile.bin
```

3. **Create a file of 10 MB**

```
fallocate -l 10M testfile.txt
```

4. **Create a file using bytes**

```
fallocate -l 1048576 one_mb_file
```

5. **Extend an existing file to 2 GB**

```
fallocate -l 2G existingfile.log
```

6. **Create a sparse file (no actual blocks allocated)**

```
fallocate -s -l 1G sparsefile.img
```

7. **Punch holes in a file (free space in the middle of a file)**

```
fallocate -p -o 100M -l 200M bigfile.dat
```

8. **Reserve disk space without initializing data**

```
fallocate -n -l 300M reservedfile.bin
```

9. **Collapse a range of a file (remove space from the middle)**

```
fallocate -c -o 50M -l 100M logfile.txt
```

10. **Insert space into a file at a specific offset**

```
fallocate -i -o 20M -l 50M report.txt
```
</details>
<details>
 <summary>dd</summary>

1. **Create a file of a specific size filled with zeros**

```
dd if=/dev/zero of=output.img bs=1M count=100
```

*Creates a 100 MB file called `output.img`.*

---

2. **Copy a disk or partition**

```
dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

*Clones the contents of `/dev/sda` to `/dev/sdb`.*

---

3. **Create a bootable USB from an ISO**

```
dd if=linux.iso of=/dev/sdb bs=4M status=progress
```

*Writes `linux.iso` directly to a USB drive (`/dev/sdb`).*

---

4. **Backup the MBR (first 512 bytes)**

```
dd if=/dev/sda of=mbr_backup.bin bs=512 count=1
```

*Backs up the Master Boot Record of `/dev/sda`.*

---

5. **Convert file format to ASCII or EBCDIC**

```
dd if=input.txt of=output.txt conv=ascii
```

*Converts the file encoding to ASCII.*

---

6. **Create a file of random data**

```
dd if=/dev/urandom of=random.bin bs=1M count=10
```

*Generates a 10 MB file of random data.*

---

7. **Wipe a disk with zeros**

```
dd if=/dev/zero of=/dev/sdc bs=1M status=progress
```

*Completely clears `/dev/sdc`.*

---

8. **Wipe a disk with random data**

```
dd if=/dev/urandom of=/dev/sdc bs=1M status=progress
```

*Securely overwrites `/dev/sdc` with random data.*

---

9. **Copy a file with block size conversion**

```
dd if=input.img of=output.img bs=512 conv=sync,noerror
```

*Copies a file using 512-byte blocks, filling missing blocks with zeros and ignoring errors.*

---

10. **Benchmark write speed of a disk**

```
dd if=/dev/zero of=testfile bs=1G count=1 oflag=direct
```

*Writes a 1 GB file directly to disk to test speed.*
</details>
<details>
 <summary>create-swap</summary>

To add 4G swap space
preallocate space to a file
```
sudo fallocate -l 4G /swapfile
```
change the permission
```
sudo chmod 600 /swapfile
```
make the swap file
```
sudo mkswap /swapfile
```
enable devices and files for paging and swapping
```
sudo swapon /swapfile
```
for persistent swap space add these parameters to fstab file
```
sudo vim /etc/fstab
```
```
/swapfile swap swap defaults 0 0
```
:wq! save and exit
```
sudo swapon --show
```
check with free command
```
free -h
```
</details>
