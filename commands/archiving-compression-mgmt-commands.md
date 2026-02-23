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
</details>
<details>
 <summary>gzip</summary>
 
The `gzip` command in Linux is used to compress and decompress files using the GNU zip compression algorithm.

## Basic Syntax

```
gzip [options] filename
```

By default, `gzip` replaces the original file with a compressed version ending in `.gz`.

### 1. Compress a file

```
gzip file.txt
```

Explanation:
Compresses `file.txt` into `file.txt.gz` and removes the original file.

---

### 2. Decompress a file

```
gzip -d file.txt.gz
```

Explanation:
Decompresses `file.txt.gz` back to `file.txt`.

---

### 3. Keep the original file while compressing

```
gzip -k file.txt
```

Explanation:
Creates `file.txt.gz` but keeps the original `file.txt`.

---

### 4. Compress multiple files

```
gzip file1.txt file2.txt
```

Explanation:
Compresses both files separately into `file1.txt.gz` and `file2.txt.gz`.

---

### 5. View compressed file contents without extracting

```
gzip -cd file.txt.gz
```

Explanation:
Decompresses and prints the content to standard output without creating a file.
</details>
<details>
 <summary>bzip2</summary>
 
The `bzip2` command in Linux is used to compress and decompress files using the Burrows–Wheeler compression algorithm, typically achieving better compression than `gzip`.

## Basic Syntax

```
bzip2 [options] filename
```

By default, `bzip2` replaces the original file with a compressed version ending in `.bz2`.

### 1. Compress a file

```
bzip2 file.txt
```

Explanation:
Compresses `file.txt` into `file.txt.bz2` and removes the original file.

---

### 2. Decompress a file

```
bzip2 -d file.txt.bz2
```

Explanation:
Decompresses `file.txt.bz2` back to `file.txt`.

---

### 3. Keep the original file while compressing

```
bzip2 -k file.txt
```

Explanation:
Creates `file.txt.bz2` but keeps the original `file.txt`.

---

### 4. Compress multiple files

```
bzip2 file1.txt file2.txt
```

Explanation:
Compresses both files separately into `file1.txt.bz2` and `file2.txt.bz2`.

---

### 5. View compressed file contents without extracting

```
bzcat file.txt.bz2
```

Explanation:
Displays the contents of `file.txt.bz2` to standard output without creating a decompressed file.
</details>
<details>
 <summary>xz</summary>
 
The `xz` command in Linux is used to compress and decompress files using the LZMA2 compression algorithm, providing high compression ratios, often better than `gzip` or `bzip2`.

## Basic Syntax

```
xz [options] filename
```

By default, `xz` replaces the original file with a compressed version ending in `.xz`.

### 1. Compress a file

```
xz file.txt
```

Explanation:
Compresses `file.txt` into `file.txt.xz` and removes the original file.

---

### 2. Decompress a file

```
xz -d file.txt.xz
```

Explanation:
Decompresses `file.txt.xz` back to `file.txt`.

---

### 3. Keep the original file while compressing

```
xz -k file.txt
```

Explanation:
Creates `file.txt.xz` but keeps the original `file.txt`.

---

### 4. Compress multiple files

```
xz file1.txt file2.txt
```

Explanation:
Compresses both files separately into `file1.txt.xz` and `file2.txt.xz`.

---

### 5. View compressed file contents without extracting

```
xz -cd file.txt.xz
```

Explanation:
Decompresses `file.txt.xz` to standard output without creating a file on disk.
</details>
<details>
 <summary>zip</summary>
 
The `zip` command in Linux is used to compress files into a single `.zip` archive, which can be easily shared or stored.

## Basic Syntax

```
zip [options] archive-name file(s)
```

By default, `zip` creates a new archive or updates an existing one.

### 1. Create a zip archive

```
zip archive.zip file1.txt file2.txt
```

Explanation:
Creates `archive.zip` containing `file1.txt` and `file2.txt`.

---

### 2. Add a file to an existing archive

```
zip archive.zip file3.txt
```

Explanation:
Adds `file3.txt` to `archive.zip` without deleting existing files.

---

### 3. Include directories recursively

```
zip -r archive.zip folder/
```

Explanation:
Compresses the `folder/` directory and all its contents into `archive.zip`.

---

### 4. Exclude certain files while zipping

```
zip -r archive.zip folder/ -x "*.log"
```

Explanation:
Compresses `folder/` but excludes all `.log` files from the archive.

---

### 5. View the contents of a zip archive

```
unzip -l archive.zip
```

Explanation:
Lists all files stored inside `archive.zip` without extracting them.
</details>
<details>
 <summary>unzip</summary>
 
The `unzip` command in Linux is used to extract files from `.zip` archives.

## Basic Syntax

```
unzip [options] archive.zip
```

By default, it extracts files into the current directory.

### 1. Extract all files from a zip archive

```
unzip archive.zip
```

Explanation:
Extracts all files from `archive.zip` into the current directory.

---

### 2. Extract to a specific directory

```
unzip archive.zip -d /path/to/destination
```

Explanation:
Extracts all files from `archive.zip` into `/path/to/destination`.

---

### 3. List contents without extracting

```
unzip -l archive.zip
```

Explanation:
Displays all files contained in the archive without extracting them.

---

### 4. Extract specific files

```
unzip archive.zip file1.txt file2.txt
```

Explanation:
Extracts only `file1.txt` and `file2.txt` from the archive.

---

### 5. Overwrite existing files without prompting

```
unzip -o archive.zip
```

Explanation:
Extracts all files and automatically overwrites any existing files in the current directory.
</details>
<details>
 <summary>7z</summary>
 
The `7z` command in Linux (from the **p7zip** package) is used to create and extract 7z archives, supporting high compression and multiple formats like `.7z`, `.zip`, `.tar`, `.gzip`, and more.

## Basic Syntax

```
7z [command] [archive name] [files...]
```

Common commands:

* `a` → add files to archive
* `x` → extract files with full paths
* `e` → extract files without paths
* `l` → list archive contents

### 1. Create a 7z archive

```
7z a archive.7z file1.txt file2.txt
```

Explanation:
Creates `archive.7z` containing `file1.txt` and `file2.txt`.

---

### 2. Extract files with full paths

```
7z x archive.7z
```

Explanation:
Extracts all files from `archive.7z`, preserving folder structure.

---

### 3. Extract files without folder structure

```
7z e archive.7z
```

Explanation:
Extracts all files from `archive.7z` into the current directory, ignoring directories.

---

### 4. List contents of an archive

```
7z l archive.7z
```

Explanation:
Shows all files and folders stored inside `archive.7z` without extracting them.

---

### 5. Compress a directory recursively

```
7z a archive.7z folder/
```

Explanation:
Adds the entire `folder/` directory and its contents into `archive.7z`.
</details>
<details>
 <summary>rar</summary>
 
The `rar` command in Linux (from the **RAR for Linux** package) is used to create and extract RAR archives, a popular compressed file format with strong compression and optional password protection.

## Basic Syntax

```
rar [command] [archive name] [files...]
```

Common commands:

* `a` → add files to archive
* `x` → extract files with full paths
* `e` → extract files without paths
* `t` → test archive integrity
* `l` → list archive contents

### 1. Create a RAR archive

```
rar a archive.rar file1.txt file2.txt
```

Explanation:
Creates `archive.rar` containing `file1.txt` and `file2.txt`.

---

### 2. Extract files with full paths

```
rar x archive.rar
```

Explanation:
Extracts all files from `archive.rar`, preserving folder structure.

---

### 3. Extract files without folder structure

```
rar e archive.rar
```

Explanation:
Extracts all files into the current directory, ignoring directories.

---

### 4. List contents of a RAR archive

```
rar l archive.rar
```

Explanation:
Displays all files stored in `archive.rar` without extracting them.

---

### 5. Test the integrity of a RAR archive

```
rar t archive.rar
```

Explanation:
Checks if `archive.rar` is valid and free from errors.
</details>
<details>
 <summary>unrar</summary>
 
The `unrar` command in Linux is used to extract files from RAR archives. It works with standard and password-protected `.rar` files.

## Basic Syntax

```
unrar [command] archive.rar [files...] [destination]
```

Common commands:

* `x` → extract files with full paths
* `e` → extract files without paths
* `l` → list archive contents
* `t` → test archive integrity

### 1. Extract all files with full paths

```
unrar x archive.rar
```

Explanation:
Extracts all files from `archive.rar`, preserving the folder structure.

---

### 2. Extract all files to a specific directory

```
unrar x archive.rar /path/to/destination/
```

Explanation:
Extracts files into `/path/to/destination/`, keeping directories intact.

---

### 3. Extract files without folder structure

```
unrar e archive.rar
```

Explanation:
Extracts all files into the current directory, ignoring subfolders.

---

### 4. List contents of a RAR archive

```
unrar l archive.rar
```

Explanation:
Displays all files contained in `archive.rar` without extracting them.

---

### 5. Test the integrity of a RAR archive

```
unrar t archive.rar
```

Explanation:
Checks if `archive.rar` is valid and free from errors before extraction.
</details>
<details>
 <summary>comparison-of-tools</summary>
 
| Command | Type               | Compression Level | Speed  | Common Use          |
| ------- | ------------------ | ----------------- | ------ | ------------------- |
| tar     | Archive            | No (alone)        | Fast   | Linux backups       |
| gzip    | Compress           | Medium            | Fast   | Logs, web files     |
| bzip2   | Compress           | High              | Slower | Larger files        |
| xz      | Compress           | Very High         | Slow   | Software packages   |
| zip     | Archive + Compress | Medium            | Fast   | Cross-platform      |
| 7z      | Archive + Compress | Very High         | Slower | Maximum compression |
</details>
