<details>
  <summary>cat</summary>
To display contents of file
```
cat /etc/group
```
To view contents of multiple files
```
cat file3.txt file4.txt
```
To create a file with cat command
```
cat > file5.txt
this is file 5
^D
```
To view cat command with large file size
```
cat file.txt | more
```
```
cat file.txt | less
```
</details>
<details>
  <summary>cd</summary>
change current directory to /etc/ssh
```
cd /etc/ssh
```
switch back to previous directory
```
cd -
```
To change current directory to parent directory
```
cd ..
```
</details>
<details>
  <summary>cak</summary>
To Show current month calendar
```
cal
```
To Show calendar of selected month and year
```
cal August 2002
```
To Show the calendar of current year with the current date highlighted
```
cal -y
```
</details>
<details>
  <summary>cp</summary>
To copying multiple files to a directory
```
cp file1_name file2_name file3_name /opt
```
To copying the files interactively
```
cp -i file_name /opt
```
To copying a directory or folder
```
cp -r /home/klug /opt/backup
```
To create symbolic links using cp command
```
cp -s /home/venus/file1.txt /opt/
```
To create hard link using cp command
```
cp -l /home/venus/file2.txt /opt/
```
</details>
<details>
  <summary>mv</summary>
To rename a file1.txt to file2.txt
```
mv file1.txt file2.txt
```
To interactively rename file1.txt to file2.txt
```
mv -i file1.txt file2.txt
```
To move multiple directories from one location to another
```
mv dir1 dir2 dir3 /opt
```
</details>
<details>
  <summary>dd</summary>
To copy a file using dd command
```
dd if=hello.txt of=output.txt status=progress
```
Convert Text File to Uppercase
```
dd if=hello.txt of=output.txt conv=ucase
```
</details>
<details>
  <summary>ln</summary>
To create hard link with the name sample_link_file.txt
```
ln sample_file.txt sample_link_file.txt
```
To unlink the created hard link
```
unlink sample_file.txt sample_link_file.txt
```
To create a soft link or symbolic link
```
ln -s file.txt link_file.txt
```
To unlink the soft link or symbolic link
```
unlink link_file.txt
```
</details>
<details>
  <summary>link</summary>
```
link file1.txt file2.txt
```
```
vim file1.txt
1 andhra
2 tamilnadu
3 kerala
4 karnataka
5 pondicherry
```
```
link file1.txt file2.txt
```
</details>
<details>
  <summary>which</summary>
```
To locate a command
which -a touch
which -a free
which -a du
which -a df
```
</details>
<details>
  <summary>whereis</summary>
To find the directories where the whereis command search
```
whereis -l
```
To get information about the commands
```
whereis du
whereis free
whereis bash
```
To get output for multiple commands
```
whereis du free bash
```
</details>
<details>
  <summary>ls</summary>
To long listing of files
```
ls -l
```
To view hidden files
```
ls -a
```
To list files with human readable format
```
ls -lh
```
</details>
<details>
  <summary>tee</summary>
To create a file that stores information about hostname
```
hostname -I | tee hostname.txt
```
To append a line of text to a file
```
echo "This is demo msg " | tee -a demo.txt
```
```
ping google.com | tee -i file.txt
```
To write to multiple files
```
echo "This is demo msg " | tee demo1.txt demo2.txt
```
</details>
<details>
  <summary> </summary>
  
</details>





















<details>
  <summary> </summary>
  
</details>
