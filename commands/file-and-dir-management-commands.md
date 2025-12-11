<details>
<summary>cat</summary>

### 1. Display a file’s contents

```bash
cat file.txt
```

### 2. Display multiple files

```bash
cat file1.txt file2.txt
```

---

## Creating Files

### 3. Create a new file (overwrite)

```bash
cat > newfile.txt
```

(Type your text, then press CTRL + D)

### 4. Append to a file

```bash
cat >> existing.txt
```

---

## Combining and Redirecting

### 5. Concatenate into a new file

```bash
cat part1.txt part2.txt > merged.txt
```

### 6. Append multiple files into one

```bash
cat a.txt b.txt >> combined.txt
```

---

## Viewing With Formatting

### 7. Show line numbers

```bash
cat -n file.txt
```

### 8. Show non-printing characters

```bash
cat -A file.txt
```

### 9. Squeeze repeated blank lines

```bash
cat -s file.txt
```

---

## Using Cat With Pipes

### 10. Pipe output into less

```bash
cat large.log | less
```

### 11. Use cat with another command

```bash
ps aux | cat
```

### 12. Duplicate output using tee

```bash
cat file.txt | tee copy.txt
```

---

## Advanced Examples

### 13. Use a here-document

```bash
cat <<EOF
line 1
line 2
line 3
EOF
```

### 14. Combine split binary files

```bash
cat archive.part* > archive.zip
```

### 15. Create a multi-line config file

```bash
cat <<EOF > config.conf
name=example
version=1.0
enabled=true
EOF
```
</details>
<details>
<summary>cd</summary>

### 1. Change to a directory

```bash
cd foldername
```

### 2. Move into a path

```bash
cd /home/user/documents
```

### 3. Go to your home directory

```bash
cd
```

or

```bash
cd ~
```

---

## Moving Relative to Current Location

### 4. Go up one directory

```bash
cd ..
```

### 5. Go up two levels

```bash
cd ../..
```

### 6. Move into a sibling directory

```bash
cd ../otherfolder
```

---

## Using Hyphen and Parent Paths

### 7. Switch back to the previous directory

```bash
cd -
```

### 8. Use `.` to refer to the current directory

```bash
cd .
```

---

## Using Absolute vs Relative Paths

### 9. Absolute path

```bash
cd /var/log
```

### 10. Relative path

```bash
cd projects/code/python
```

---

## Using Variables and Special Paths

### 11. Go to the root directory

```bash
cd /
```

### 12. Go to a user’s home directory

```bash
cd ~username
```

### 13. Use an environment variable

```bash
cd $HOME/projects
```

---

## Combining With Quotes

### 14. Directory with spaces

```bash
cd "My Projects/2024 Work"
```

---

## Practical Examples

### 15. Move to the directory of a script

```bash
cd "$(dirname myscript.sh)"
```

### 16. Move to the desktop

```bash
cd ~/Desktop
```

### 17. Move to a mounted drive

```bash
cd /mnt/usb
```
</details>
<details>
<summary>cal</summary>

### 1. Show the current month

```bash
cal
```

### 2. Show a specific year

```bash
cal 2025
```

### 3. Show a specific month of a specific year

```bash
cal 03 2025
```

(March 2025)

---

## Formatting Options

### 4. Display Monday as the first day of the week

```bash
cal -m 1
```

### 5. Display weeks with week numbers

```bash
cal -w
```

### 6. Weeks + Monday start

```bash
cal -w -m 1
```

---

## Display Ranges

### 7. Show the previous, current, and next month

```bash
cal -3
```

### 8. Show 12 months (full year)

```bash
cal -y
```

### 9. Show 12 months of a given year

```bash
cal -y 2030
```

---

## Julian Dates

### 10. Show Julian calendar days

```bash
cal -j
```

### 11. Julian days for a specific month/year

```bash
cal -j 7 2024
```

---

## Handy Practical Uses

### 12. Check a specific month next year

```bash
cal 6 2026
```

### 13. Show three months for a specific date

```bash
cal -3 2 2025
```
</details>
<details>
<summary>cp</summary>

### 1. Copy a file

```bash
cp file.txt backup.txt
```

### 2. Copy a file to a directory

```bash
cp file.txt /home/user/Documents/
```

### 3. Copy multiple files to a directory

```bash
cp file1.txt file2.txt /home/user/backup/
```

---

## Copying Directories

### 4. Copy a directory recursively

```bash
cp -r folder1 folder1_backup
```

### 5. Copy a directory into another directory

```bash
cp -r photos/ /mnt/usb/
```

---

## Overwrite Controls

### 6. Ask before overwriting

```bash
cp -i file.txt existing.txt
```

### 7. Do not overwrite existing files

```bash
cp -n file.txt existing.txt
```

### 8. Force overwrite (useful in scripts)

```bash
cp -f file.txt target.txt
```

---

## Preserve Attributes

### 9. Preserve permissions, timestamps, ownership

```bash
cp -p file.txt backup.txt
```

### 10. Keep everything exactly (archive mode)

```bash
cp -a source/ backup/
```

Equivalent to: `-r -p` and more.

---

## Verbose Output

### 11. Show each copy action

```bash
cp -v file.txt backup.txt
```

### 12. Verbose recursive copy

```bash
cp -rv src/ dest/
```

---

## Wildcards and Patterns

### 13. Copy all text files

```bash
cp *.txt /backup/
```

### 14. Copy files beginning with "log"

```bash
cp log* /var/log/archive/
```

---

## Practical Examples

### 15. Copy a config file before editing

```bash
cp /etc/nginx/nginx.conf nginx.conf.bak
```

### 16. Copy a directory to a USB drive

```bash
cp -a /home/user/Documents /mnt/usb/
```

### 17. Copy only newer files (overwrite only if newer)

```bash
cp -u *.txt /backup/
```
</details>
<details>
<summary>mv</summary>

### 1. Rename a file

```bash
mv oldname.txt newname.txt
```

### 2. Move a file to a directory

```bash
mv file.txt /home/user/Documents/
```

### 3. Move multiple files to a directory

```bash
mv file1.txt file2.txt /home/user/archive/
```

---

## Moving Directories

### 4. Move a directory

```bash
mv folder1 folder2
```

### 5. Move a directory into another directory

```bash
mv project/ /mnt/usb/
```

---

## Overwrite Options

### 6. Ask before overwriting

```bash
mv -i file.txt existing.txt
```

### 7. Do not overwrite existing files

```bash
mv -n file.txt existing.txt
```

### 8. Force overwrite without prompting

```bash
mv -f file.txt destination.txt
```

---

## Verbose Output

### 9. Show what is being moved

```bash
mv -v file.txt /backup/
```

### 10. Verbose for multiple items

```bash
mv -v *.log logs/
```

---

## Wildcards and Patterns

### 11. Move all text files

```bash
mv *.txt /backup/
```

### 12. Move files starting with "img"

```bash
mv img* photos/
```

---

## Practical Examples

### 13. Rename a directory

```bash
mv old_project new_project
```

### 14. Move everything from one directory to another

```bash
mv * /destination/
```

### 15. Sort files by extension

```bash
mv *.jpg images/
mv *.mp3 music/
```

### 16. Move only newer files

```bash
mv -u *.txt /backup/
```

### 17. Move files into the parent directory

```bash
mv file.txt ..
```
</details>
<details>
<summary>dd</summary>

### 1. Copy a file (simple file-to-file copy)

```bash
dd if=input.bin of=output.bin
```

### 2. Convert text to uppercase while copying

```bash
dd if=source.txt of=upper.txt conv=ucase
```

---

## Block Size & Performance

### 3. Copy with a larger block size (faster)

```bash
dd if=input.iso of=output.iso bs=4M
```

### 4. Limit amount of data copied (example: first 100 MB)

```bash
dd if=bigfile.bin of=small.bin bs=1M count=100
```

---

## Backing Up (Safe Examples)

### 5. Create a compressed backup of a file

```bash
dd if=largefile.img | gzip > backup.img.gz
```

### 6. Read from a device safely (non-destructive read)

```bash
dd if=/dev/sda bs=4M | gzip > disk_backup.gz
```

(Reading is safe; the danger is when writing **to** a device.)

---

## Progress & Stats

### 7. Show progress while running

```bash
dd if=input.iso of=copy.iso bs=4M status=progress
```

### 8. Get speed stats only at the end

```bash
dd if=source of=target bs=1M status=none
```

---

## Data Testing (Safe)

### 9. Generate a file filled with zeros (100 MB test file)

```bash
dd if=/dev/zero of=testfile.bin bs=1M count=100
```

### 10. Generate a file filled with random data (slower)

```bash
dd if=/dev/urandom of=random.bin bs=1M count=10
```

---

## ISO / Image Handling

### 11. Verify two images are identical

```bash
dd if=image1.iso of=compare.bin bs=4M
cmp compare.bin image2.iso
```

### 12. Extract a portion of an image (first 1 MB)

```bash
dd if=disk.img of=header.bin bs=1M count=1
```

---

## Dangerous Operations (Shown With Safe Warnings)

**These examples are common system admin tasks but can destroy data if misused.
Use them **only** if you are certain about device names.**

### 13. Write an ISO to a USB drive

(Example only — ensure `/dev/sdX` is correct.)

```bash
dd if=linux.iso of=/dev/sdX bs=4M status=progress
```

### 14. Clone one disk to another

(Again, double-check device names.)

```bash
dd if=/dev/sda of=/dev/sdb bs=64K status=progress
```

---

## Advanced Useful Examples

### 15. Benchmark disk read speed

```bash
dd if=/dev/sda of=/dev/null bs=1M count=1024 status=progress
```

### 16. Wipe a file by overwriting it (single pass)

```bash
dd if=/dev/zero of=secret.txt bs=1M
```
</details>
<details>
<summary>ln</summary>

### 1. Create a hard link

```bash
ln original.txt hardlink.txt
```

Both files now point to the same data.

### 2. Create a hard link inside a directory

```bash
ln file.txt backup/hardlink.txt
```

### 3. List files with inode numbers (to verify hard links)

```bash
ls -li file.txt hardlink.txt
```

---

## Symbolic (Soft) Link Examples

### 4. Create a symbolic link

```bash
ln -s target.txt link.txt
```

### 5. Symlink to a directory

```bash
ln -s /var/log logs
```

### 6. Create a symlink using a relative path

```bash
ln -s ../images/logo.png logo.png
```

---

## Overwrite and Force Options

### 7. Force create or replace a symlink

```bash
ln -sfn new_target linkname
```

### 8. Ask before replacing an existing symlink

```bash
ln -si file.txt link.txt
```

---

## Practical Everyday Uses

### 9. Make a shorter name for a long path

```bash
ln -s /opt/software/version_10.2.4/bin appbin
```

### 10. Link config directories across systems

```bash
ln -s ~/.config/nvim ~/.vim
```

### 11. Link a shared resource

```bash
ln -s /shared/media/videos myvideos
```

---

## Advanced Examples

### 12. Create multiple symlinks at once

```bash
ln -s *.log logs/
```

### 13. Update a broken symlink

```bash
ln -sf new/location/config.yml config.yml
```

### 14. Create a hard link to a file in another directory

```bash
ln /home/user/file.txt /home/user/documents/hardlink.txt
```

### 15. Symlink executable into /usr/local/bin

```bash
ln -s ~/projects/tool/run.sh /usr/local/bin/tool
```
</details>
<details>
<summary>link</summary>

### 1. Create a hard link

```bash
link original.txt hardlink.txt
```

Equivalent to:

```bash
ln original.txt hardlink.txt
```

but without any safety options.

---

## Verifying Hard Links

### 2. Check inode numbers to confirm the link

```bash
ls -li original.txt hardlink.txt
```

They should have the same inode number.

---

## Linking Files in Different Directories

### 3. Create a hard link inside another directory

```bash
link /home/user/data.txt /home/user/backup/data_link.txt
```

### 4. Link a file from a shared location

```bash
link /shared/config.yml /home/user/config.yml
```

---

## Error Handling Examples

### 5. Attempting to link across filesystems (will fail)

```bash
link /mnt/disk1/file.txt /mnt/disk2/file.txt
```

Hard links **cannot** cross filesystem boundaries.

### 6. Attempting to link to a directory (not allowed)

```bash
link /var/log /home/user/log_link
```

Hard links to directories are blocked to prevent filesystem loops.

---

## Practical Use Cases

### 7. Create a backup pointer without duplicating data

```bash
link report.pdf report_backup.pdf
```

### 8. Create multiple access points to the same file

```bash
link ~/notes/today.txt ~/Desktop/today.txt
```

### 9. Use hard links as a simple versioning trick

```bash
cp --reflink=auto file.txt file_v2.txt
link file_v2.txt file_v3.txt
```
</details>
<details>
<summary>unlink</summary>

### 1. Remove a file

```bash
unlink file.txt
```

### 2. Remove a symbolic link

```bash
unlink mylink
```

(The target file or directory remains untouched.)

---

## Practical Symlink Examples

### 3. Remove a symlink to a directory

```bash
unlink logs
```

### 4. Remove a broken symlink

```bash
unlink old_target_link
```

---

## Using Full Paths

### 5. Unlink using an absolute path

```bash
unlink /home/user/project/tempfile
```

### 6. Remove a link inside another directory

```bash
unlink ~/bin/tool
```

---

## Safe Checks Before Unlinking

### 7. Check if a file is a symlink before removing

```bash
[ -L linkname ] && unlink linkname
```

### 8. Check if a file exists before unlinking

```bash
[ -e file.txt ] && unlink file.txt
```

---

## Hard Link Scenario

### 9. Remove one hard link (file data stays until last link is removed)

```bash
unlink hardlink.txt
```

The original file remains unless it was the last link.

---

## Error Case Examples (common mistakes)

### 10. Attempting to remove a directory (will fail)

```bash
unlink myfolder
```

`unlink: cannot unlink 'myfolder': Is a directory`

### 11. Attempting to remove multiple files (not allowed)

```bash
unlink file1 file2
```
</details>
<details>
<summary>which</summary>

### 1. Find the path of a command

```bash
which ls
```

Output might be:

```
/bin/ls
```

### 2. Find the path of another command

```bash
which python3
```

Output might be:

```
/usr/bin/python3
```

---

## Multiple Commands

### 3. Find paths of multiple commands at once

```bash
which gcc make python3
```

Outputs paths for each command found in `$PATH`.

---

## Using Options

### 4. Show all occurrences in `$PATH` (`-a` for all)

```bash
which -a python3
```

Outputs all locations of `python3` in the path, not just the first one.

---

## Practical Uses

### 5. Verify if a command exists

```bash
which git
```

If no output, the command is not installed or not in `$PATH`.

### 6. Debug PATH issues

```bash
which java
```

Helps confirm which version of Java is being executed if multiple are installed.

### 7. Use in scripts

```bash
editor=$(which vim)
$editor myfile.txt
```
</details>
<details>
<summary>whereis</summary>

### 1. Locate the binary, source, and man page of a command

```bash
whereis ls
```

Example output:

```
ls: /bin/ls /usr/share/man/man1/ls.1.gz
```

### 2. Locate only the binary

```bash
whereis -b gcc
```

Output might be:

```
gcc: /usr/bin/gcc
```

### 3. Locate only the source

```bash
whereis -s bash
```

Output might be:

```
bash: /usr/src/bash
```

### 4. Locate only the man pages

```bash
whereis -m python3
```

Output might be:

```
python3: /usr/share/man/man1/python3.1.gz
```

---

## Searching Multiple Commands

### 5. Locate multiple commands at once

```bash
whereis ls grep awk
```

Outputs paths for each of the commands found.

---

## Limiting the Search Path

### 6. Search only in specific directories

```bash
whereis -B /bin:/usr/bin ls
```

Searches only in `/bin` and `/usr/bin`.

---

## Practical Uses

### 7. Verify installation of a command

```bash
whereis git
```

If nothing is found, the command may not be installed.

### 8. Find manual pages for a command

```bash
whereis -m vim
```

### 9. Locate all relevant files for troubleshooting

```bash
whereis -b -m -s perl
```
</details>
<details>
<summary>ls</summary>

### 1. List files in the current directory

```bash
ls
```

### 2. List files with detailed information

```bash
ls -l
```

Shows permissions, owner, group, size, and modification date.

### 3. List all files including hidden ones

```bash
ls -a
```

Hidden files start with `.`

### 4. List all files in long format including hidden files

```bash
ls -la
```

---

## Sorting and Formatting

### 5. List files sorted by modification time

```bash
ls -lt
```

### 6. List files sorted by size

```bash
ls -lS
```

### 7. List files in reverse order

```bash
ls -lr
```

### 8. List human-readable file sizes

```bash
ls -lh
```

Shows sizes like `K`, `M`, `G` instead of bytes.

### 9. Combine options (long + human-readable + sorted by size)

```bash
ls -lhS
```

---

## Directory Listing

### 10. List contents of a specific directory

```bash
ls /var/log
```

### 11. List recursively all files in directories

```bash
ls -R
```

### 12. List only directories

```bash
ls -d */
```

---

## Pattern Matching

### 13. List all `.txt` files

```bash
ls *.txt
```

### 14. List files starting with `log`

```bash
ls log*
```

### 15. List files containing `report`

```bash
ls *report*
```

---

## Practical Examples

### 16. List files sorted by modification date, newest first

```bash
ls -lt
```

### 17. List only files larger than a certain size (with `ls` + `find`)

```bash
find . -type f -size +1M -exec ls -lh {} \;
```

### 18. List hidden configuration files in home directory

```bash
ls -d ~/.* 
```
</details>
<details>
<summary>lsattr</summary>

### 1. List attributes of a single file

```bash
lsattr file.txt
```

Example output:

```
----i--------e-- file.txt
```

Here `i` means the file is **immutable**.

### 2. List attributes of all files in a directory

```bash
lsattr *
```

### 3. List attributes recursively for all files

```bash
lsattr -R
```

---

## Common Options

### 4. Show only user-readable output (compact)

```bash
lsattr -a
```

Includes hidden files starting with `.`

### 5. Display attributes for a specific directory

```bash
lsattr /var/log
```

---

## Practical Examples

### 6. Check if a file is immutable

```bash
lsattr important.txt
```

Look for the `i` attribute.

### 7. Verify files before backup

```bash
lsattr /home/user/Documents/*
```

### 8. Check attributes in a system directory

```bash
lsattr /etc
```

---

## Notes on Attributes

* Common attribute letters:

  * `i` → immutable (cannot be modified, deleted, or renamed)
  * `a` → append-only (can only append data)
  * `c` → compressed
  * `e` → extent format
* Use `chattr` to **change file attributes**.
</details>
<details>
<summary>mkdir</summary>

### 1. Create a single directory

```bash
mkdir myfolder
```

### 2. Create multiple directories at once

```bash
mkdir folder1 folder2 folder3
```

---

## Creating Nested Directories

### 3. Create nested directories in one command

```bash
mkdir -p parent/child/grandchild
```

`-p` creates parent directories if they don’t exist.

### 4. Create multiple nested directories at once

```bash
mkdir -p project/{src,bin,docs}
```

Creates `project/src`, `project/bin`, and `project/docs`.

---

## Permissions

### 5. Set permissions while creating a directory

```bash
mkdir -m 755 newfolder
```

`755` = owner can read/write/execute, others can read/execute.

---

## Practical Examples

### 6. Create a directory for logs

```bash
mkdir /var/log/myapp
```

### 7. Create a temporary workspace

```bash
mkdir -p ~/workspace/project1
```

### 8. Combine with `date` to create timestamped directories

```bash
mkdir -p ~/backup/$(date +%Y-%m-%d)
```

Creates a directory like `backup/2025-12-11`.

### 9. Create directories for multiple users

```bash
mkdir /home/{alice,bob,charlie}
```

### 10. Create a directory and immediately move into it

```bash
mkdir newproject && cd newproject
```
</details>
<details>
<summary>rmdir</summary>

### 1. Remove a single empty directory

```bash
rmdir myfolder
```

### 2. Remove multiple empty directories at once

```bash
rmdir folder1 folder2 folder3
```

---

## Removing Nested Directories

### 3. Remove a nested empty directory

```bash
rmdir parent/child/grandchild
```

The directory must be empty; otherwise, it will fail.

### 4. Remove parent directories if they are empty

```bash
rmdir -p parent/child/grandchild
```

Removes `grandchild`, then `child`, then `parent` if they are all empty.

---

## Practical Examples

### 5. Remove an empty temporary directory

```bash
rmdir /tmp/workspace
```

### 6. Remove directories after cleaning up files

```bash
rm file.txt
rmdir myfolder
```

### 7. Combine with `find` to remove empty directories recursively

```bash
find /home/user/project -type d -empty -exec rmdir {} \;
```

---

## Notes

* `rmdir` **cannot remove directories with files** inside. Use `rm -r` for non-empty directories.
* `rmdir -p` is useful for cleaning up nested empty directories in one command.
</details>
<details>
<summary>rm</summary>

`rm` is used to **remove files and directories**. Be careful, as deleted files are usually **not recoverable**.

### 1. Remove a single file

```bash
rm file.txt
```

### 2. Remove multiple files

```bash
rm file1.txt file2.txt file3.txt
```

---

## Using Options for Safety

### 3. Ask before removing each file

```bash
rm -i file.txt
```

### 4. Remove files without confirmation (force)

```bash
rm -f file.txt
```

### 5. Remove multiple files with prompt for each

```bash
rm -i *.log
```

---

## Removing Directories

### 6. Remove an empty directory

```bash
rmdir folder
```

or, using `rm`:

```bash
rm -d folder
```

### 7. Remove a directory and all its contents recursively

```bash
rm -r myfolder
```

### 8. Force remove a directory and contents without confirmation

```bash
rm -rf myfolder
```

---

## Pattern Matching

### 9. Remove all `.txt` files in a directory

```bash
rm *.txt
```

### 10. Remove files starting with `temp`

```bash
rm temp*
```

### 11. Remove all hidden files in a directory

```bash
rm -rf .*
```

(Be careful with this—it can remove `.` or `..` if used incorrectly.)

---

## Practical Examples

### 12. Clean up a downloads folder

```bash
rm ~/Downloads/*.zip
```

### 13. Remove all log files older than 7 days

```bash
find /var/log -type f -name "*.log" -mtime +7 -exec rm -f {} \;
```

### 14. Delete temporary project folder

```bash
rm -rf ~/workspace/project_temp
```

### 15. Remove a file only if it exists

```bash
rm -f file.txt
```

---

## Notes

* Always double-check **`rm -rf`**—it can permanently delete important data.
* Use `-i` for safety in scripts or when working in critical directories.
</details>
<details>
<summary>less</summary>

`less` is a pager program used to **view text files one screen at a time**. It’s often preferred over `more` because it allows both forward and backward navigation.

### 1. View a file

```bash
less file.txt
```

### 2. View multiple files

```bash
less file1.txt file2.txt
```

---

## Navigating Inside `less`

* Scroll down one line: `↓` or `Enter`
* Scroll up one line: `↑`
* Scroll down one page: `Space`
* Scroll up one page: `b`
* Go to the beginning: `g`
* Go to the end: `G`
* Search for text: `/pattern`
* Repeat search forward: `n`
* Repeat search backward: `N`
* Exit `less`: `q`

---

## Options with `less`

### 3. Show line numbers while viewing

```bash
less -N file.txt
```

### 4. View a file with case-insensitive search

```bash
less -I file.txt
```

### 5. View a file with raw control characters (for colored output)

```bash
less -R file.txt
```

---

## Viewing Command Output

### 6. Pipe command output into `less`

```bash
ps aux | less
```

### 7. View long log files

```bash
cat /var/log/syslog | less
```

### 8. View compressed files without decompressing manually

```bash
zless /var/log/syslog.1.gz
```

---

## Practical Examples

### 9. Search and highlight pattern while viewing

```bash
less +/error /var/log/syslog
```

Opens the file and jumps to the first occurrence of `error`.

### 10. Start viewing from a specific line

```bash
less +100 file.txt
```

Starts at line 100.

### 11. Follow a growing log file (like `tail -f`)

```bash
less +F /var/log/syslog
```

Press `Ctrl+C` to stop following, `F` to resume.
</details>
<details>
<summary>more</summary>

`more` is a pager used to **view text files one screen at a time**. It’s simpler than `less` but still useful for quick viewing.

### 1. View a file

```bash
more file.txt
```

### 2. View multiple files

```bash
more file1.txt file2.txt
```

---

## Navigating Inside `more`

* Scroll down one line: `Enter`
* Scroll down one page: `Space`
* Scroll up one page: `b`
* Go to the beginning: `g`
* Search forward for text: `/pattern`
* Repeat search: `n`
* Exit `more`: `q`

---

## Using with Commands

### 3. Pipe command output into `more`

```bash
ls -l | more
```

### 4. View a long log file

```bash
cat /var/log/syslog | more
```

### 5. Show the output of `dmesg` one screen at a time

```bash
dmesg | more
```

---

## Options

### 6. Display line numbers while viewing

```bash
more -d file.txt
```

Displays prompts like `"Press space to continue, 'q' to quit."`

### 7. Pause after a certain number of lines

```bash
more -n 20 file.txt
```

Pauses after every 20 lines instead of the default page size.

---

## Practical Examples

### 8. View command history

```bash
history | more
```

### 9. View large directory listing

```bash
ls -lR /etc | more
```

### 10. Search for a keyword in a file while viewing

```bash
more file.txt
```

Then type `/keyword` and press `Enter`.

---

**Notes:**

* `more` allows only forward navigation by default (backward is limited).
* For more advanced navigation (forward/backward, search, follow file growth), `less` is recommended.
</details>
<details>
<summary>pwd</summary>

`pwd` (print working directory) shows the **absolute path of the current directory**.

### 1. Display the current working directory

```bash
pwd
```

Example output:

```
/home/user/Documents
```

---

## Options

### 2. Print the logical path (default behavior)

```bash
pwd -L
```

Shows the path based on symbolic links.

### 3. Print the physical path

```bash
pwd -P
```

Resolves all symbolic links to show the real physical path.

---

## Practical Examples

### 4. Use in a script to store current directory

```bash
current_dir=$(pwd)
echo "The script is running in $current_dir"
```

### 5. Combine with other commands

```bash
ls $(pwd)
```

Lists files in the current directory explicitly.

### 6. Print path while changing directories

```bash
cd /var/log && pwd
```

Outputs:

```
/var/log
```

### 7. Display physical path of a symlinked directory

```bash
cd /home/user/link_to_folder
pwd -P
```

Shows the actual folder location.

---

## Notes

* `pwd` is a **simple but essential command** for scripts and navigation.
* `pwd -L` vs `pwd -P` is important when working with symbolic links.
</details>
<details>
<summary>stat</summary>

`stat` displays **detailed information about files and directories**, including size, permissions, timestamps, and inode info.

### 1. Show detailed info of a file

```bash
stat file.txt
```

Example output:

```
  File: file.txt
  Size: 1024       Blocks: 8          IO Block: 4096   regular file
Device: 803h/2051d Inode: 123456      Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/ user)   Gid: ( 1000/ user)
Access: 2025-12-11 12:34:56.000000000 +0000
Modify: 2025-12-10 09:21:00.000000000 +0000
Change: 2025-12-10 09:21:01.000000000 +0000
 Birth: -
```

### 2. Show info for a directory

```bash
stat /home/user/Documents
```

---

## Formatting Output

### 3. Display only file size

```bash
stat -c %s file.txt
```

### 4. Display only last modification time

```bash
stat -c %y file.txt
```

### 5. Display multiple info with a format

```bash
stat -c "Name: %n, Size: %s bytes, Permissions: %A, Modified: %y" file.txt
```

---

## Practical Examples

### 6. Check inode number

```bash
stat -c %i file.txt
```

### 7. Compare timestamps of two files

```bash
stat -c "%n: %y" file1.txt file2.txt
```

### 8. Use in scripts to verify file size

```bash
filesize=$(stat -c %s file.txt)
echo "File size: $filesize bytes"
```

### 9. Display major and minor device numbers for a device file

```bash
stat -c "Device: %t:%T" /dev/sda1
```

### 10. Show all available attributes for a file

```bash
stat -x file.txt    # on BSD/macOS
stat file.txt       # on Linux
```

---

## Notes

* `%n` → file name
* `%s` → file size in bytes
* `%A` → human-readable permissions
* `%y` → last modification time
* `%i` → inode number
* `%U` → owner name, `%G` → group name
</details>
<details>
<summary>tail</summary>

`tail` is used to **view the last part of a file**, commonly logs or outputs of growing files.

### 1. Display the last 10 lines of a file (default)

```bash
tail file.txt
```

### 2. Display the last `n` lines

```bash
tail -n 20 file.txt
```

Shows the last 20 lines.

---

## Follow File Updates

### 3. Follow a file in real-time (like `tail -f`)

```bash
tail -f /var/log/syslog
```

Shows new lines as they are added.

### 4. Follow with number of lines

```bash
tail -n 50 -f /var/log/syslog
```

Starts with the last 50 lines and then follows new updates.

---

## From the Beginning or by Bytes

### 5. Display last `n` bytes

```bash
tail -c 100 file.txt
```

Shows the last 100 bytes instead of lines.

### 6. Display from a specific line number

```bash
tail -n +10 file.txt
```

Shows from line 10 to the end.

---

## Multiple Files

### 7. Tail multiple files at once

```bash
tail -n 20 file1.log file2.log
```

Displays the last 20 lines of each file with a header.

### 8. Follow multiple files

```bash
tail -f access.log error.log
```

Shows live updates for both files.

---

## Practical Examples

### 9. Monitor system logs for a keyword

```bash
tail -f /var/log/syslog | grep "error"
```

### 10. Save last 100 lines to a new file

```bash
tail -n 100 file.txt > last100.txt
```

### 11. Combine with `sleep` in a script

```bash
while true; do tail -n 10 /var/log/syslog; sleep 5; done
```

Shows the last 10 lines every 5 seconds.

---

**Notes:**

* `tail -f` is especially useful for **log monitoring**.
* `tail -n +N` is good for **skipping initial lines**.
* `tail -c` is useful when working with **binary or fixed-length files**.
</details>
<details>
<summary>head</summary>

`head` is used to **view the first part of a file**, commonly for logs, text files, or outputs.

### 1. Display the first 10 lines of a file (default)

```bash
head file.txt
```

### 2. Display the first `n` lines

```bash
head -n 20 file.txt
```

Shows the first 20 lines.

---

## By Bytes

### 3. Display the first `n` bytes

```bash
head -c 100 file.txt
```

Shows the first 100 bytes of the file.

---

## Multiple Files

### 4. Head multiple files at once

```bash
head -n 5 file1.txt file2.txt
```

Shows the first 5 lines of each file with headers.

---

## Practical Examples

### 5. Preview a log file

```bash
head -n 50 /var/log/syslog
```

Shows the first 50 lines to check recent entries.

### 6. Combine with `grep` to search only the beginning

```bash
head -n 100 file.txt | grep "ERROR"
```

Searches for `ERROR` only in the first 100 lines.

### 7. Display the first 20 lines of all `.log` files

```bash
head -n 20 *.log
```

### 8. Check file headers in CSV or text files

```bash
head -n 5 data.csv
```

Useful for quickly viewing column names or formatting.

---

## Notes

* `head` is complementary to `tail`; use `head` for the **start of files**, `tail` for the **end**.
* Options:

  * `-n` → number of lines
  * `-c` → number of bytes
</details>
<details>
<summary>tee</summary>

The `tee` command reads from **standard input** and writes to **both standard output and files simultaneously**. It’s useful for logging while displaying output.

### 1. Write command output to a file

```bash
echo "Hello World" | tee file.txt
```

* Displays `Hello World` on the terminal and writes it to `file.txt`.

### 2. Append to a file instead of overwriting

```bash
echo "New Line" | tee -a file.txt
```

* `-a` appends to the file instead of replacing it.

---

## Using `tee` with Commands

### 3. Save the output of `ls` to a file

```bash
ls -l | tee listing.txt
```

### 4. Save and append system info

```bash
uname -a | tee -a system_info.txt
```

### 5. Combine multiple commands with `tee`

```bash
(disk_usage=$(df -h); echo "$disk_usage") | tee disk_report.txt
```

---

## With Sudo

### 6. Write to a file requiring root privileges

```bash
echo "127.0.0.1 mylocal.test" | sudo tee -a /etc/hosts
```

* Useful because `sudo` alone doesn’t affect the redirection `>`.

---

## Practical Examples

### 7. Log output of a script while showing it

```bash
./backup.sh | tee backup.log
```

### 8. Save only errors while still displaying them

```bash
./run_program 2>&1 | tee program_output.log
```

### 9. Use `tee` with multiple files

```bash
echo "Important info" | tee file1.txt file2.txt
```

* Writes the same content to multiple files and shows it on the terminal.

---

## Notes

* `tee` is especially useful in **scripts and pipelines**.
* `-a` → append mode
* Without `-a`, `tee` **overwrites** the file.
</details>
<details>
<summary>touch</summary>

The `touch` command is mainly used to **create empty files** or **update file timestamps**.

### 1. Create a single empty file

```bash
touch file.txt
```

### 2. Create multiple empty files at once

```bash
touch file1.txt file2.txt file3.txt
```

---

## Update Timestamps

### 3. Update access and modification time of a file

```bash
touch file.txt
```

* If the file exists, its **timestamps are updated** without changing contents.

### 4. Set a specific timestamp

```bash
touch -t 202512110930 file.txt
```

* Sets the modification time to **2025-12-11 09:30**.

### 5. Set timestamps to match another file

```bash
touch -r reference.txt file.txt
```

* Makes `file.txt` have the same timestamps as `reference.txt`.

---

## Practical Examples

### 6. Create a log file if it doesn’t exist

```bash
touch /var/log/myapp.log
```

### 7. Update multiple files’ timestamps in a project

```bash
touch src/*.c src/*.h
```

### 8. Combine with `find` to update timestamps of all `.txt` files

```bash
find . -name "*.txt" -exec touch {} \;
```

### 9. Create a new file with a date-based name

```bash
touch report_$(date +%Y-%m-%d).txt
```

* Creates a file like `report_2025-12-11.txt`.

---

## Notes

* `touch` **does not modify file contents** when updating timestamps.
* `-c` → do not create a file if it doesn’t exist
* `-a` → change access time only
* `-m` → change modification time only
</details>
<details>
<summary>xargs</summary>

`xargs` is used to **build and execute command lines from standard input**, often in combination with `find`, `grep`, or `echo`.

### 1. Echo items from input

```bash
echo "one two three" | xargs
```

Output:

```
one two three
```

### 2. Pass input as arguments to a command

```bash
echo "file1.txt file2.txt" | xargs ls -l
```

* Runs `ls -l file1.txt file2.txt`.

---

## Using with `find`

### 3. Remove files found by `find`

```bash
find . -name "*.tmp" | xargs rm
```

* Deletes all `.tmp` files in the current directory tree.

### 4. Count lines in multiple files

```bash
find . -name "*.txt" | xargs wc -l
```

* Counts lines in all `.txt` files found.

### 5. Handle filenames with spaces

```bash
find . -name "*.log" -print0 | xargs -0 rm
```

* `-print0` and `xargs -0` handle filenames containing spaces or newlines safely.

---

## Limiting Arguments

### 6. Run a command with a limited number of arguments at a time

```bash
cat files.txt | xargs -n 2 echo
```

* Prints 2 filenames per line.

### 7. Run commands in parallel

```bash
cat files.txt | xargs -n 1 -P 4 gzip
```

* Compresses files using up to 4 parallel processes.

---

## Practical Examples

### 8. Copy files listed in a text file

```bash
cat filelist.txt | xargs -I {} cp {} /backup/
```

* `-I {}` replaces `{}` with each line from input.

### 9. Delete all empty files listed by `find`

```bash
find . -type f -empty | xargs rm
```

### 10. Search and delete files interactively

```bash
find . -name "*.bak" | xargs -p rm
```

* `-p` asks for confirmation before each `rm`.

---

## Notes

* `xargs` is extremely useful when combined with `find`, `grep`, or `echo`.
* `-0` → handle null-separated input (safe for spaces/newlines)
* `-n` → number of arguments per command
* `-P` → number of parallel processes
* `-I` → replace placeholder with input
</details>
<details>
<summary>find</summary>

`find` is used to **search for files and directories** based on various criteria like name, type, size, permissions, and more.

### 1. Find files by name

```bash
find /path/to/search -name "file.txt"
```

* Searches for `file.txt` in `/path/to/search` and subdirectories.

### 2. Find files by pattern

```bash
find . -name "*.log"
```

* Finds all `.log` files in the current directory and subdirectories.

---

## Searching by Type

### 3. Find directories only

```bash
find . -type d
```

### 4. Find regular files only

```bash
find . -type f
```

### 5. Find symbolic links

```bash
find . -type l
```

---

## Searching by Size

### 6. Find files larger than 100MB

```bash
find / -type f -size +100M
```

### 7. Find files smaller than 1KB

```bash
find . -type f -size -1k
```

---

## Searching by Time

### 8. Find files modified in the last 7 days

```bash
find . -type f -mtime -7
```

### 9. Find files accessed more than 30 days ago

```bash
find . -type f -atime +30
```

### 10. Find files changed within the last 1 hour

```bash
find . -type f -cmin -60
```

---

## Searching by Permissions

### 11. Find files with 777 permissions

```bash
find . -type f -perm 777
```

### 12. Find files not writable by others

```bash
find . -type f ! -perm -o=w
```

---

## Executing Commands on Found Files

### 13. Delete all `.tmp` files

```bash
find . -name "*.tmp" -type f -exec rm {} \;
```

### 14. Move all `.log` files to a backup directory

```bash
find . -name "*.log" -type f -exec mv {} /backup/ \;
```

### 15. Count lines in all `.txt` files

```bash
find . -name "*.txt" -type f -exec wc -l {} \;
```

---

## Combining with `xargs`

### 16. Remove files safely with spaces in names

```bash
find . -name "*.bak" -print0 | xargs -0 rm
```

### 17. Search and compress files

```bash
find . -name "*.log" -type f -print0 | xargs -0 gzip
```

---

## Practical Examples

### 18. Find empty files

```bash
find . -type f -empty
```

### 19. Find directories named `backup`

```bash
find / -type d -name "backup"
```

### 20. Find files owned by a specific user

```bash
find /home -type f -user alice
```

---

## Notes

* `-type` → f=file, d=directory, l=symlink
* `-mtime`, `-atime`, `-cmin` → filter by time
* `-perm` → filter by permissions
* `-exec` → run a command on each found file
* Use `-print0` with `xargs -0` to handle filenames with spaces safely
</details>
<details>
<summary>updatedb</summary>

`updatedb` is used to **update the database for the `locate` command**, which allows fast file searching.

### 1. Update the `locate` database (default)

```bash
sudo updatedb
```

* Scans the filesystem and updates `/var/lib/mlocate/mlocate.db` (or similar).

### 2. Update without sudo (user-specific database)

```bash
updatedb --localpaths='/home/user'
```

* Updates only paths under `/home/user`.

---

## Excluding Paths

### 3. Exclude specific directories from the database

```bash
sudo updatedb --prunepaths='/tmp /var/tmp /mnt'
```

* Directories `/tmp`, `/var/tmp`, and `/mnt` are skipped.

### 4. Exclude filesystems like `nfs` or `proc`

```bash
sudo updatedb --prunefs='nfs proc'
```

---

## Using Environment Variables

### 5. Update database using custom environment variables

```bash
export PRUNEPATHS="/tmp /media"
sudo updatedb
```

* Skips `/tmp` and `/media` directories.

### 6. Limit database to certain paths

```bash
sudo updatedb --localpaths='/usr /etc'
```

* Only indexes `/usr` and `/etc`.

---

## Practical Examples

### 7. Update database quietly (no output)

```bash
sudo updatedb -q
```

### 8. Update database and check last modification time

```bash
sudo updatedb && ls -l /var/lib/mlocate/mlocate.db
```

### 9. Schedule automatic database update (cron)

```bash
sudo crontab -e
```

Add line:

```bash
0 3 * * * /usr/bin/updatedb
```

* Updates database every day at 3 AM.

---

## Notes

* `updatedb` **must be run as root** to index all directories (or with appropriate permissions).
* Database location: `/var/lib/mlocate/mlocate.db` (on most systems).
* Combined with `locate`, it allows **fast file searches**:

```bash
locate file.txt
```
</details>
<details>
<summary>locate</summary>

`locate` is used to **find files quickly** using a database (updated by `updatedb`), rather than scanning the filesystem in real time.

### 1. Find a file by name

```bash
locate file.txt
```

* Lists all paths containing `file.txt`.

### 2. Find files by pattern

```bash
locate "*.log"
```

* Lists all `.log` files in the database.

---

## Searching with Options

### 3. Limit the number of results

```bash
locate -n 10 "*.conf"
```

* Shows only the first 10 matches.

### 4. Case-insensitive search

```bash
locate -i "README"
```

* Finds files ignoring case (`README`, `readme`, etc.).

### 5. Show only existing files

```bash
locate -e "*.sh"
```

* Only lists files that currently exist.

---

## Using Patterns

### 6. Find files in a specific directory

```bash
locate /home/user/*.txt
```

* Searches only within `/home/user`.

### 7. Use wildcards to search recursively

```bash
locate "/var/log/*.log"
```

---

## Practical Examples

### 8. Find configuration files

```bash
locate "*.conf" | grep nginx
```

* Finds configuration files related to `nginx`.

### 9. Search for recently created files

```bash
locate "*.pdf" | xargs ls -lt | head -n 10
```

* Shows the 10 most recent PDF files.

### 10. Search and delete files (careful!)

```bash
locate "*.bak" | xargs rm -i
```

* Finds all `.bak` files and asks before deleting each one.

### 11. Find files excluding a pattern

```bash
locate "*.log" | grep -v old
```

* Excludes results containing `old`.

---

## Notes

* `locate` is **much faster than `find`**, but relies on the database.
* Update the database before searching for new files:

```bash
sudo updatedb
```

* Useful options:

  * `-n <num>` → limit results
  * `-i` → ignore case
  * `-e` → show only existing files
</details>
<details>
<summary>realpath</summary>

`realpath` is used to **display the absolute path of a file or directory**, resolving all symbolic links.

### 1. Show absolute path of a file

```bash
realpath file.txt
```

Output example:

```
/home/user/Documents/file.txt
```

### 2. Show absolute path of a directory

```bash
realpath ./myfolder
```

Output example:

```
/home/user/Documents/myfolder
```

---

## Resolving Symbolic Links

### 3. Resolve symbolic links to the actual path

```bash
realpath symlink.txt
```

* If `symlink.txt` points to `/var/log/file.txt`, `realpath` outputs the real target.

### 4. Resolve a symlinked directory

```bash
realpath mylink/
```

* Displays the physical path of the directory, not the symlink.

---

## Using with Commands

### 5. Combine with `cd` and `pwd`

```bash
cd myfolder
realpath .
```

* Shows the full path of the current directory.

### 6. Convert relative paths to absolute paths in a script

```bash
file="./notes.txt"
absolute_path=$(realpath "$file")
echo $absolute_path
```

---

## Practical Examples

### 7. Show absolute paths of multiple files

```bash
realpath file1.txt file2.txt file3.txt
```

### 8. Find absolute path of a command

```bash
realpath $(which ls)
```

* Shows the absolute path to the `ls` executable.

### 9. Resolve nested symlinks

```bash
realpath symlink1
```

* Resolves symlink1 → symlink2 → actual file.

### 10. Use in combination with `find`

```bash
find . -name "*.txt" -exec realpath {} \;
```

* Lists absolute paths for all `.txt` files found.

---

## Notes

* `realpath` always returns **full absolute paths**.
* Useful in scripts for **resolving symlinks and working with absolute paths**.
* If a file does not exist, `realpath` may return an error unless `-m` (canonicalize missing) is used:

```bash
realpath -m nonexistingfile.txt
```
</details>









