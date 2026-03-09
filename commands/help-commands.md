## 1. `man`

Displays the manual page for a command with full documentation.

Examples:

```
man ls
man grep
man systemctl
```

In Linux, **`man` sections (1–8)** organize manual pages by category. You can specify a section number to open the correct manual page.

Syntax:

```
man <section_number> <command>
```

---

### 1. Section 1 – User Commands

Contains commands that normal users can run from the shell.

Examples:

```
man 1 ls
man 1 cp
man 1 grep
```

Explanation: Shows documentation for common user-level commands.

---

### 2. Section 2 – System Calls

Describes functions provided by the Linux kernel (used in programming).

Examples:

```
man 2 open
man 2 read
man 2 fork
```

Explanation: Shows how programs interact directly with the kernel.

---

### 3. Section 3 – Library Functions

Documentation for functions in system libraries such as the C standard library.

Examples:

```
man 3 printf
man 3 malloc
man 3 strcmp
```

Explanation: Used mainly by developers writing programs in C or other languages.

---

### 4. Section 4 – Special Files / Device Files

Information about special files usually located in `/dev`.

Examples:

```
man 4 null
man 4 tty
man 4 random
```

Explanation: Describes device interfaces and hardware-related files.

---

### 5. Section 5 – File Formats and Configuration Files

Documentation for system configuration files and their formats.

Examples:

```
man 5 passwd
man 5 fstab
man 5 crontab
```

Explanation: Explains structure and meaning of configuration files.

---

### 6. Section 6 – Games and Screensavers

Manual pages for games and fun programs included in Linux systems.

Examples:

```
man 6 fortune
man 6 tetris
man 6 nethack
```

Explanation: Contains documentation for system games and entertainment utilities.

---

### 7. Section 7 – Miscellaneous

Includes conventions, protocols, and standards used in Linux.

Examples:

```
man 7 tcp
man 7 signal
man 7 socket
```

Explanation: Provides conceptual documentation and system conventions.

---

### 8. Section 8 – System Administration Commands

Commands mainly used by system administrators for system maintenance.

Examples:

```
man 8 fdisk
man 8 mount
man 8 reboot
```

Explanation: Shows documentation for administrative and root-level commands.

---

Example of specifying section when multiple entries exist:

```
man 1 passwd
man 5 passwd
```
```
`man 1 passwd` → command to change password
`man 5 passwd` → format of `/etc/passwd` file.
```
---

## 2. `help`

Shows help information for built-in shell commands (mainly in bash).

Examples:

```
help cd
help history
help export
```

---

## 3. `command --help`

Displays a quick usage guide and options for a command.

Examples:

```
ls --help
cp --help
tar --help
```

---

## 4. `info`

Shows detailed documentation in GNU info format.

Examples:

```
info ls
info bash
info coreutils
```

---

## 5. `whatis`

Displays a short one-line description of a command from the manual database.

Examples:

```
whatis ls
whatis passwd
whatis tar
```

---

## 6. `apropos`

Searches the manual page descriptions for keywords.

Examples:

```
apropos copy
apropos network
apropos password
```

---

## 7. `type`

Shows how the shell interprets a command (alias, builtin, file, or function).

Examples:

```
type ls
type cd
type python
```

---

## 8. `which`

Shows the full path of the executable command being used.

Examples:

```
which python
which ls
which docker
```

---

## 9. `whereis`

Finds the binary, source, and manual page files for a command.

Examples:

```
whereis ls
whereis python
whereis nginx
```

---

## 10. `tldr`

Shows simplified examples of common command usage.

Examples:

```
tldr tar
tldr git
tldr docker
```

---

## 11. `--usage`

Displays short usage information for some commands.

Examples:

```
grep --usage
mkdir --usage
chmod --usage
```

---

## 12. `compgen -c`

Lists all available commands in the shell.

Examples:

```
compgen -c
compgen -c | grep git
compgen -c | wc -l
```
