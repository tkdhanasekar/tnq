<details>
 <summary>tar</summary>

`tar` (Tape Archive) is a Linux command used to **create, extract, compress, decompress, and manage archive files** such as `.tar`, `.tar.gz`, `.tar.bz2`, and `.tar.xz`.

### 1) Create a tar archive

```bash
tar -cvf archive.tar file1.txt file2.txt
```

Creates `archive.tar` containing `file1.txt` and `file2.txt`.

---

### 2) Extract a tar archive

```bash
tar -xvf archive.tar
```

Extracts all files from `archive.tar`.

---

### 3) Create a gzip compressed archive

```bash
tar -czvf archive.tar.gz myfolder/
```

Creates a `.tar.gz` archive of `myfolder/`.

---

### 4) Extract a gzip compressed archive

```bash
tar -xzvf archive.tar.gz
```

Extracts a `.tar.gz` archive.

---

### 5) Create a bzip2 compressed archive

```bash
tar -cjvf archive.tar.bz2 myfolder/
```

Creates a `.tar.bz2` archive using bzip2 compression.

---

### 6) Extract a bzip2 compressed archive

```bash
tar -xjvf archive.tar.bz2
```

Extracts a `.tar.bz2` archive.

---

### 7) Create an xz compressed archive

```bash
tar -cJvf archive.tar.xz myfolder/
```

Creates a `.tar.xz` archive using xz compression.

---

### 8) Extract an xz compressed archive

```bash
tar -xJvf archive.tar.xz
```

Extracts a `.tar.xz` archive.

---

### 9) List contents of an archive without extracting

```bash
tar -tvf archive.tar
```

Displays the contents of `archive.tar`.

---

### 10) Extract archive to a specific directory

```bash
tar -xvf archive.tar -C /path/to/destination/
```

Extracts files into `/path/to/destination/` directory.
</details>
<details>
 <summary>cpio</summary>
 
The `cpio` command in Linux is used to copy files to and from archives. It is commonly used for creating archive files, extracting archives, and copying files between directories.

---

## Basic Syntax

```
cpio [options]
```

`cpio` works in three main modes:

* Copy-out mode (`-o`) – create an archive
* Copy-in mode (`-i`) – extract an archive
* Copy-pass mode (`-p`) – copy files from one directory to another

---

### 1. Create an archive (copy-out mode)

```
find . -name "*.txt" | cpio -o > archive.cpio
```

Explanation:
Finds all `.txt` files in the current directory and creates `archive.cpio`.

---

### 2. Extract files from an archive (copy-in mode)

```
cpio -i < archive.cpio
```

Explanation:
Extracts all files from `archive.cpio` into the current directory.

---

### 3. Extract files with verbose output

```
cpio -iv < archive.cpio
```

Explanation:
Extracts files and displays each filename as it is processed.

---

### 4. Extract specific files from an archive

```
cpio -i "*.txt" < archive.cpio
```

Explanation:
Extracts only `.txt` files from the archive.

---

### 5. Copy files from one directory to another (copy-pass mode)

```
find src_dir -type f | cpio -pdm dest_dir
```

Explanation:
Copies all files from `src_dir` to `dest_dir`, creating directories as needed (`-d`) and preserving modification times (`-m`).
