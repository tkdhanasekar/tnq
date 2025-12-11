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

