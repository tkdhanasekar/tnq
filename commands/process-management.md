<details>
 <summary>bg</summary>

`bg` resumes a **stopped job in the background**, allowing it to keep running without occupying the terminal.

> **Reminder:**
> `bg` works with **jobs**, not PIDs, and is used after `Ctrl+Z`.

---

1. **Resume the most recent stopped job**

```bash
bg
```

Continues the last stopped job in the background.

2. **Resume a specific job**

```bash
bg %1
```

Resumes job number `1` in the background.

3. **List jobs before using bg**

```bash
jobs
```

Shows job numbers and their states.

4. **Stop a running foreground job**

```bash
Ctrl+Z
```

Suspends the current job (puts it in “Stopped” state).

5. **Stop → background workflow**

```bash
sleep 300
Ctrl+Z
bg
```

Runs `sleep` in the background after stopping it.

6. **Background a long-running command**

```bash
tar -czf backup.tar.gz /data
Ctrl+Z
bg
```

7. **Check background job status**

```bash
jobs -l
```

Shows job IDs with PIDs.

8. **Bring a job back to foreground**

```bash
fg %1
```

Moves job `1` back to the foreground.

9. **Run multiple jobs in background**

```bash
command1 &
command2 &
```

Starts jobs directly in the background (no `bg` needed).

10. **Background a stopped editor**

```bash
vim file.txt
Ctrl+Z
bg
```
</details>
<details>
 <summary>crontab</summary>

`crontab` is used to **schedule commands or scripts to run automatically at specified times and intervals**.

1. **Edit the current user’s crontab**

```bash
crontab -e
```

Opens the crontab file in the default editor.

2. **List the current user’s cron jobs**

```bash
crontab -l
```

Displays all scheduled jobs for the current user.

3. **Remove the current user’s crontab**

```bash
crontab -r
```

Deletes all cron jobs for the current user.

4. **Edit another user’s crontab (root only)**

```bash
sudo crontab -e -u username
```

5. **Run a script every day at midnight**

```bash
0 0 * * * /path/to/script.sh
```

6. **Run a command every 5 minutes**

```bash
*/5 * * * * /usr/bin/command
```

7. **Run a job every Sunday at 2:30 AM**

```bash
30 2 * * 0 /path/to/backup.sh
```

8. **Run a job at system reboot**

```bash
@reboot /path/to/startup.sh
```

9. **Redirect output to a log file**

```bash
0 1 * * * /path/to/script.sh >> /var/log/script.log 2>&1
```

10. **Set environment variables in crontab**

```bash
PATH=/usr/local/bin:/usr/bin:/bin
```

---

### Cron time format reminder

```
* * * * *
| | | | |
| | | | └── Day of week (0–7, Sunday = 0 or 7)
| | | └──── Month (1–12)
| | └────── Day of month (1–31)
| └──────── Hour (0–23)
└────────── Minute (0–59)
```
</details>
<details>
 <summary>fg</summary>

`fg` brings a **background or stopped job to the foreground**, attaching it to the current terminal.

1. **Bring the most recent job to the foreground**

```bash
fg
```

2. **List current jobs**

```bash
jobs
```

Shows job numbers needed for `fg`.

3. **Bring a specific job to the foreground**

```bash
fg %1
```

Moves job number `1` to the foreground.

4. **Bring another job to the foreground**

```bash
fg %2
```

5. **Stop a foreground job**

```bash
Ctrl+Z
```

Suspends the running job.

6. **Stop then foreground a job**

```bash
sleep 300
Ctrl+Z
fg
```

7. **Foreground a background-running job**

```bash
command &
fg
```

8. **Foreground a job using part of its name**

```bash
fg %vim
```

Brings the job whose command starts with `vim` to the foreground.

9. **View job PIDs**

```bash
jobs -l
```

Shows both job numbers and process IDs.

10. **Foreground a stopped editor**

```bash
vim file.txt
Ctrl+Z
fg
```
</details>
<details>
 <summary>cron</summary>

`cron` is the **background daemon that executes scheduled jobs** defined in crontab files at specified times.

1. **Check cron service status**

```bash
systemctl status cron
```

Shows whether the cron daemon is running.

2. **Start the cron service**

```bash
sudo systemctl start cron
```

3. **Stop the cron service**

```bash
sudo systemctl stop cron
```

4. **Enable cron at boot**

```bash
sudo systemctl enable cron
```

5. **Restart cron after changes**

```bash
sudo systemctl restart cron
```

6. **View cron logs**

```bash
grep CRON /var/log/syslog
```

Shows executed cron jobs (Debian/Ubuntu).

7. **View cron logs on RHEL-based systems**

```bash
grep CRON /var/log/cron
```

8. **List system-wide cron directories**

```bash
ls /etc/cron.*
```

Shows hourly, daily, weekly, and monthly cron jobs.

9. **View system crontab**

```bash
cat /etc/crontab
```

Displays system-level scheduled jobs and their users.

10. **Check user cron spool**

```bash
ls /var/spool/cron/
```

Shows per-user crontab files.
</details>
<details>
 <summary>fc</summary>

`fc` edits, lists, or re-executes **commands from the shell command history**.

1. **Edit the most recent command and run it**

```bash
fc
```

2. **Edit the last command using the default editor**

```bash
fc -e vi
```

3. **List the last 10 commands**

```bash
fc -l -10
```

4. **List commands with line numbers**

```bash
fc -l
```

5. **Re-run the previous command without editing**

```bash
fc -s
```

6. **Re-run the previous command with substitution**

```bash
fc -s old=new
```

Replaces `old` with `new` in the last command and executes it.

7. **Edit a specific command by number**

```bash
fc 120
```

Edits and runs command number `120` from history.

8. **Edit a range of commands**

```bash
fc 120 125
```

Edits and executes commands from history lines 120 to 125.

9. **Use a different editor**

```bash
fc -e nano
```

10. **List commands without line numbers**

```bash
fc -ln
```
</details>
<details>
 <summary>fuser</summary>

`fuser` identifies **processes that are using a file, directory, or filesystem**.

1. **Find processes using a file**

```bash
fuser /var/log/syslog
```

2. **Find processes using a directory**

```bash
fuser /home
```

3. **Show detailed output**

```bash
fuser -v /var/log/syslog
```

Displays user, PID, access type, and command.

4. **Identify processes using a mounted filesystem**

```bash
fuser /mnt/data
```

5. **Kill processes using a file**

```bash
fuser -k /mnt/data
```

6. **Kill processes using a filesystem forcefully**

```bash
fuser -km /mnt/data
```

Kills all processes accessing the mounted filesystem.

7. **Show access type**

```bash
fuser -v /mnt/data
```

Shows how the process is using the resource (read, write, execute).

8. **Find processes using a TCP port**

```bash
fuser 80/tcp
```

9. **Kill process using a TCP port**

```bash
fuser -k 8080/tcp
```

10. **Check UDP port usage**

```bash
fuser 53/udp
```
</details>
<details>
 <summary>jobs</summary>

`jobs` lists **background and stopped jobs** started in the current shell session.

1. **List all jobs**

```bash
jobs
```

2. **List jobs with job IDs and status**

```bash
jobs -l
```

Shows job numbers along with their PIDs.

3. **List jobs with process group IDs**

```bash
jobs -p
```

Displays only the PIDs of jobs.

4. **Show only running jobs**

```bash
jobs -r
```

5. **Show only stopped jobs**

```bash
jobs -s
```

6. **Start a job in the background**

```bash
command &
```

7. **Stop a foreground job**

```bash
Ctrl+Z
```

8. **Restart a stopped job in the background**

```bash
bg %1
```

9. **Bring a background job to the foreground**

```bash
fg %1
```

10. **Check job states after logout protection**

```bash
disown -a
```

Removes all jobs from the shell’s job table.
</details>
<details>
 <summary>kill</summary>

`kill` sends a **signal to a process** (usually to terminate it) using its process ID or job ID.

1. **Terminate a process gracefully**

```bash
kill 1234
```

Sends `SIGTERM` (signal 15) to process `1234`.

2. **Send a specific signal**

```bash
kill -SIGTERM 1234
```

3. **Forcefully terminate a process**

```bash
kill -9 1234
```

Sends `SIGKILL` (signal 9).

4. **List all available signals**

```bash
kill -l
```

5. **Send a signal by number**

```bash
kill -15 1234
```

6. **Kill a background job using job ID**

```bash
kill %1
```

7. **Stop (pause) a running process**

```bash
kill -STOP 1234
```

8. **Resume a stopped process**

```bash
kill -CONT 1234
```

9. **Kill multiple processes**

```bash
kill 1234 5678 9012
```

10. **Kill all processes owned by a user**

```bash
kill -9 -1
```

Kills all processes you own (use with extreme caution).
</details>
<details>
 <summary>kill -9</summary>

`kill -9` forcefully **terminates a process immediately** by sending the `SIGKILL` signal, bypassing cleanup.

1. **Force-kill a process by PID**

```bash
kill -9 1234
```

2. **Kill multiple processes**

```bash
kill -9 1234 5678 9012
```

3. **Kill a background job**

```bash
kill -9 %1
```

4. **Kill a frozen or unresponsive process**

```bash
kill -9 $(pidof firefox)
```

5. **Kill all instances of a program**

```bash
kill -9 $(pgrep apache2)
```

6. **Kill a process running on a specific port**

```bash
kill -9 $(fuser 8080/tcp)
```

7. **Kill a child process tree**

```bash
kill -9 -1234
```

Sends `SIGKILL` to the entire process group.

8. **Kill all processes owned by the current user**

```bash
kill -9 -1
```

Terminates all processes you own (dangerous).

9. **Use sudo to kill another user’s process**

```bash
sudo kill -9 4321
```

10. **Verify the process is gone**

```bash
ps -p 1234
```
</details>
<details>
 <summary>killall</summary>

`killall` sends a **signal to all processes matching a given name**, usually to terminate them.

1. **Terminate all processes by name**

```bash
killall firefox
```

2. **Send a specific signal**

```bash
killall -SIGTERM nginx
```

3. **Forcefully kill all matching processes**

```bash
killall -9 chrome
```

4. **Kill processes owned by a specific user**

```bash
killall -u john python
```

5. **List processes that would be killed (dry run)**

```bash
killall -v ssh
```

6. **Case-insensitive process name match**

```bash
killall -I firefox
```

7. **Kill processes older than a certain time**

```bash
killall -o 2h java
```

Kills Java processes older than 2 hours.

8. **Kill processes newer than a certain time**

```bash
killall -y 10m node
```

9. **Wait for processes to terminate**

```bash
killall -w apache2
```

10. **Kill processes quietly**

```bash
killall -q vim
```
</details>
<details>
 <summary>lsof</summary>

`lsof` lists **open files and the processes that opened them**, including files, directories, sockets, and network connections.

1. **List all open files**

```bash
lsof
```

2. **Show open files for a specific process**

```bash
lsof -p 1234
```

3. **Show processes using a specific file**

```bash
lsof /var/log/syslog
```

4. **Show open files in a directory**

```bash
lsof +D /home/user
```

5. **List open files by a user**

```bash
lsof -u john
```

6. **Show network connections**

```bash
lsof -i
```

7. **Show processes using a TCP port**

```bash
lsof -i :80
```

8. **Show only TCP connections**

```bash
lsof -i tcp
```

9. **Show deleted but still open files**

```bash
lsof | grep deleted
```

10. **Find processes preventing unmount**

```bash
lsof /mnt/data
```
</details>
<details>
 <summary>top</summary>

`top` displays **real-time system information**, including CPU, memory usage, and running processes.

1. **Start top with default view**

```bash
top
```

2. **Sort processes by memory usage**

```bash
top -o %MEM
```

3. **Sort processes by CPU usage**

```bash
top -o %CPU
```

4. **Display processes for a specific user**

```bash
top -u john
```

5. **Show full command lines**

```bash
top -c
```

6. **Batch mode for logging**

```bash
top -b -n 1
```

Outputs a snapshot once for scripts or logs.

7. **Change refresh interval (e.g., 5 seconds)**

```bash
top -d 5
```

8. **Kill a process from top**

* Press `k`, then enter the PID.

9. **Highlight running tasks**

* Press `z` in interactive mode.

10. **Filter tasks by name**

* Press `o` and type `COMMAND=python` inside top.
</details>
<details>
 <summary>htop</summary>

`htop` is an **interactive, colorized process viewer** that displays CPU, memory, and system resource usage in real-time, with easier navigation than `top`.

1. **Start `htop`**

```bash
htop
```

2. **Sort processes by CPU usage**

* Press `F6` or click the CPU column header.

3. **Sort processes by memory usage**

* Press `F6` and select `%MEM`.

4. **Search for a process**

* Press `F3`, type the process name.

5. **Filter processes by user**

* Press `F4`, then type the username.

6. **Kill a process**

* Select a process and press `F9`.

7. **Change priority (nice) of a process**

* Select a process and press `F7` (increase) or `F8` (decrease).

8. **Tree view of processes**

* Press `F5` to toggle tree view.

9. **Batch mode for scripts**

```bash
htop -b -n 1
```

Outputs a snapshot once, suitable for logging.

10. **Monitor specific user’s processes**

```bash
htop -u john
```
</details>
<details>
 <summary>uptime</summary>

`uptime` shows **how long the system has been running**, along with the current time, number of users, and load averages.

1. **Display basic uptime**

```bash
uptime
```

2. **Show only the current time**

```bash
uptime -p
```

Outputs a human-readable format like "up 3 hours, 25 minutes".

3. **Show since when the system has been up**

```bash
uptime -s
```

Displays system boot time.

4. **Include load averages**

```bash
uptime
```

Default output includes 1, 5, and 15-minute load averages.

5. **Monitor uptime in a loop**

```bash
watch uptime
```

Updates the uptime every 2 seconds.

6. **Check uptime on a remote machine**

```bash
ssh user@host uptime
```

7. **Combine with awk to get only load average**

```bash
uptime | awk -F'load average: ' '{ print $2 }'
```

8. **Display uptime in a short human-readable form**

```bash
uptime -p
```

Outputs something like: "up 2 days, 4 hours".

9. **Display uptime in seconds (script-friendly)**

```bash
cat /proc/uptime
```

First value shows total seconds since boot.

10. **Monitor load trends along with uptime**

```bash
uptime; top -b -n 1 | head -10
```

Shows uptime and top resource-consuming processes.
</details>
<details>
 <summary>atop</summary>

`atop` is an **advanced, real-time system and process monitor** that tracks CPU, memory, disk, and network usage, including historical logging.

1. **Start `atop` in interactive mode**

```bash
atop
```

2. **Show CPU usage per process**

* Run `atop` and press `c` to toggle CPU view.

3. **Show memory usage per process**

* Press `m` inside `atop`.

4. **Show disk I/O per process**

* Press `d` inside `atop`.

5. **Show network usage per process**

* Press `n` inside `atop`.

6. **Run `atop` in logging mode (record system activity)**

```bash
atop -w /var/log/atop.log 60
```

Logs system activity every 60 seconds.

7. **Read previously recorded `atop` logs**

```bash
atop -r /var/log/atop.log
```

8. **Display only processes consuming CPU above a threshold**

```bash
atop -P 90
```

Shows processes using more than 90% CPU.

9. **Monitor a specific process**

```bash
atop -p 1234
```

10. **Combine `atop` with batch mode for scripts**

```bash
atop -b -n 1
```

Outputs one snapshot suitable for parsing or logging.
</details>
<details>
 <summary>&</summary>

`&` is used to **run a command in the background**, allowing the terminal to accept new commands immediately.

1. **Run a simple command in the background**

```bash
sleep 60 &
```

2. **Run a long script in the background**

```bash
./backup.sh &
```

3. **Run multiple commands in the background**

```bash
command1 & command2 &
```

4. **Check background jobs**

```bash
jobs
```

5. **Bring a background job to the foreground**

```bash
fg %1
```

6. **Stop a foreground job and move it to the background**

```bash
Ctrl+Z
bg
```

7. **Run a command in the background and disown it**

```bash
./long_task.sh & disown
```

Keeps it running even after logging out.

8. **Redirect output of a background command**

```bash
./backup.sh > backup.log 2>&1 &
```

9. **Run a GUI program in the background**

```bash
gedit & 
```

10. **Run a process in the background and get its PID**

```bash
sleep 120 & echo $!
```

Outputs the process ID of the background command.
</details>
<details>
 <summary>w</summary>

`w` shows **who is logged in and what they are doing**, along with system uptime, load averages, and user activity.

1. **Display logged-in users and activity**

```bash
w
```

2. **Show only usernames**

```bash
w -h
```

Omits the header line.

3. **Show detailed information**

```bash
w -f
```

Includes the remote hostname.

4. **Show information for a specific user**

```bash
w john
```

5. **Display idle times of users**

```bash
w
```

Idle time is in the `idle` column.

6. **Check system uptime and load averages**

```bash
w
```

The first line shows uptime and load averages.

7. **Monitor logged-in users repeatedly**

```bash
watch w
```

Updates every 2 seconds.

8. **Show TTY of users**

```bash
w
```

TTY is displayed in the second column.

9. **Combine with grep to find a user**

```bash
w | grep john
```

10. **Check system activity remotely**

```bash
ssh user@host w
```
</details>
<details>
 <summary>lsns</summary>

`lsns` lists **Linux namespaces**, showing the namespace type, ID, owner processes, and related information.

1. **List all namespaces**

```bash
lsns
```

2. **List namespaces with process IDs**

```bash
lsns -p
```

3. **Show only user namespaces**

```bash
lsns -t user
```

4. **Show only mount namespaces**

```bash
lsns -t mnt
```

5. **Show only network namespaces**

```bash
lsns -t net
```

6. **Show only PID namespaces**

```bash
lsns -t pid
```

7. **Show only IPC namespaces**

```bash
lsns -t ipc
```

8. **List namespaces for a specific process**

```bash
lsns -p 1234
```

9. **Display namespaces with tree view**

```bash
lsns -T
```

10. **Output in numeric format**

```bash
lsns -n
```

Shows namespace IDs instead of symbolic names.
</details>
<details>
 <summary>nice</summary>

`nice` **starts a process with a specified CPU scheduling priority (niceness)**, affecting how the system allocates CPU time.

1. **Start a process with default niceness (0)**

```bash
nice command
```

2. **Start a process with lower priority**

```bash
nice -n 10 command
```

3. **Start a process with higher priority (requires root)**

```bash
sudo nice -n -5 command
```

4. **Run a CPU-heavy script politely**

```bash
nice -n 15 ./backup.sh
```

5. **Run a compilation in the background with low priority**

```bash
nice -n 19 make -j4 &
```

6. **Check the current process niceness**

```bash
ps -o pid,ni,cmd -p 1234
```

7. **Start a command and log output**

```bash
nice -n 10 ./long_task.sh > task.log 2>&1
```

8. **Combine with `nohup` to run long tasks after logout**

```bash
nohup nice -n 10 ./backup.sh &
```

9. **Start a high-priority interactive task**

```bash
sudo nice -n -10 top
```

10. **Run multiple commands with low priority**

```bash
nice -n 10 command1; nice -n 10 command2
```
* Niceness ranges from -20 (highest priority) to 19 (lowest priority).
* Regular users can increase niceness (lower priority); decreasing niceness requires root.
* Use nice to prevent CPU-heavy tasks from slowing down critical processes.
</details>
<details>
 <summary>renice</summary>

`renice` **changes the CPU scheduling priority (niceness) of running processes**, allowing dynamic adjustment of their priority.

1. **Increase niceness (lower priority) of a process**

```bash
renice 10 -p 1234
```

2. **Decrease niceness (higher priority, requires root)**

```bash
sudo renice -5 -p 1234
```

3. **Change priority of multiple processes**

```bash
renice 5 -p 1234 5678 9012
```

4. **Change priority of all processes of a user**

```bash
renice 10 -u john
```

5. **Change priority of all processes in a process group**

```bash
renice 15 -g 1001
```

6. **Check current niceness of a process before changing**

```bash
ps -o pid,ni,cmd -p 1234
```

7. **Increase priority for a CPU-heavy job temporarily**

```bash
sudo renice -10 -p 4321
```

8. **Lower priority of background tasks**

```bash
renice 19 -p $(pgrep long_task)
```

9. **Adjust priority of processes started by another user (requires root)**

```bash
sudo renice 5 -u alice
```

10. **Verify changes after renice**

```bash
ps -o pid,ni,cmd -p 1234
```
* Niceness ranges from **-20 (highest priority)** to **19 (lowest priority)**.
* Increasing niceness reduces CPU priority; decreasing it increases CPU priority.
* Useful for **dynamically managing system load and prioritizing important tasks**.
</details>
<details>
 <summary>nohup</summary>

`nohup` runs a command **immune to hangups**, allowing it to continue running after logout or terminal closure.

1. **Run a command that continues after logout**

```bash
nohup ./backup.sh &
```

2. **Redirect output to a file**

```bash
nohup ./backup.sh > backup.log 2>&1 &
```

3. **Run a long-running script in the background**

```bash
nohup python3 long_task.py &
```

4. **Start a server process**

```bash
nohup java -jar server.jar > server.log 2>&1 &
```

5. **Combine with `nice` to lower priority**

```bash
nohup nice -n 10 ./backup.sh > backup.log 2>&1 &
```

6. **Run a command for another user (requires sudo)**

```bash
sudo -u john nohup ./script.sh &
```

7. **Check running `nohup` processes**

```bash
ps -ef | grep script.sh
```

8. **Use nohup with `sleep` for testing**

```bash
nohup sleep 300 &
```

9. **Run a GUI program without terminal**

```bash
nohup gedit &
```

10. **Ensure processes survive terminal crash**

```bash
nohup ./critical_task.sh > critical.log 2>&1 &
```

---

### Key notes

* Output is written to `nohup.out` by default if not redirected.
* Often combined with `&` for background execution.
* Essential for **long-running scripts, remote sessions, and server tasks**.
</details>
<details>
 <summary>pidof</summary>

`pidof` **returns the process ID(s) (PID) of a running program** by its name.

1. **Get the PID of a single process**

```bash
pidof sshd
```

2. **Get PIDs of all instances of a program**

```bash
pidof apache2
```

3. **Use PID to check if a process is running**

```bash
if pidof nginx >/dev/null; then echo "Running"; fi
```

4. **Kill a process using pidof**

```bash
kill $(pidof firefox)
```

5. **Force kill all instances of a program**

```bash
kill -9 $(pidof chrome)
```

6. **Check multiple processes**

```bash
pidof sshd mysqld
```

7. **Use PID in scripts**

```bash
PID=$(pidof python)
echo "Python is running with PID $PID"
```

8. **Check if a daemon is running before restarting**

```bash
pidof httpd || systemctl start httpd
```

9. **Combine with `ps` to view process details**

```bash
ps -fp $(pidof java)
```

10. **Monitor multiple processes using PID**

```bash
top -p $(pidof mysqld)
```
</details>
