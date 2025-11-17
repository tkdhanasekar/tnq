<details>
  <summary>adduser</summary>
  
To add a user:
```
adduser doe
```
To add a user doe with a different shell zsh:
```
sudo adduser doe --shell /bin/zsh
```
To add a user doe with different home directory thirstyminds:
```
sudo adduser doe --home /home/thirstyminds/
```
To Add a existing user doe to a Specific Group devops
```
sudo adduser doe devops
```
</details>
<details>
  <summary>addgroup</summary>

To add a new group devops
```
sudo addgroup devops
```
To Create a System Group
```
sudo addgroup --system nginx
```
To View Group Information
```
grep devops /etc/group
```
</details>
<details>
  <summary>delgroup</summary>

To delete an user account doe and Keep Home Directory
```
sudo deluser doe
```
To delete a user doe and their home directory
```
sudo deluser --remove-home doe
```
To remove a user doe from a specific group devops
```
sudo deluser doe devops
```
To delete user account doe and backup the doe’s home directory into /backup_dir
```
sudo deluser --backup-to /backup_dir doe
```
</details>
<details>
  <summary>delgroup</summary>

To remove a group devops from the system
```
sudo delgroup devops
```
To Delete a System Group
```
sudo delgroup --system nginx
```
```
sudo delgroup --system apache
```
To Simulate Group Deletion of devops
```
sudo delgroup --dry-run devops
```
</details>
<details>
  <summary>useradd</summary>

To add a new user doe
```
sudo useradd doe
```
To Create a user doe with a home directory /home/doe
```
sudo useradd -m doe
```
To create a User doe with a Specific User ID 1007
```
sudo useradd -u 1007 doe
```
To Create a User doe with Account Expiry Date
```
sudo useradd -e 2025-12-31 doe
```
To check
```
chage -l doe
```
</details>
<details>
  <summary>userdel</summary>
  
To delete a user account doe
```
sudo userdel doe
```
To remove the user’s and home directory and mail spool of user doe
```
sudo userdel -r doe
```
</details>
<details>
  <summary>usermod</summary>

To add supplementary and primary group to user
```
sudo usermod -aG sudo doe
```
To set user account expiry date
```
sudo usermod -e 2025-12-31 doe
```
To lock user account
```
sudo usermod -L doe
```
To unlock user account
```
sudo usermod -U doe
```
</details>
<details>
  <summary>groupadd</summary>

To create a group devops
```
sudo groupadd devops
```
To create a group devops with specific groupid
```
sudo groupadd devops -g 1234
```
To Verify Group Creation
```
grep devops /etc/group
```
</details>
<details>
  <summary>groupdel</summary>

To delete a group
```
sudo groupdel developers
```
To verify group deletion
```
getent group developers
```
</details>
<details>
  <summary>groupmod</summary>
  
To change the group “devops” to “developers”
```
sudo groupmod -n developers devops
```
To change groupid of a group devops to 1234
```
sudo groupmod -g 1234 devops
```
</details>
<details>
  <summary>groupmems</summary>
  
To list all members of a group developers
```
sudo groupmems -g developers -l
```
To make the user doe a member of the group devops
```
sudo groupmems -g devops -a doe
```
To delete/remove a user doc from a group devops
```
sudo groupmems -g devops -d doe
```
</details>
<details>
  <summary>gpasswd</summary>
  
To set a group password
```
sudo gpasswd developers
```
To give user alice administrative rights to the group developers
```
sudo gpasswd -A alice developers
```
To lock a group developers
```
sudo gpasswd -r developers
```
</details>
<details>
  <summary>passwd</summary>
  
To change password for root
```
sudo passwd root
```
To display user status Information of doe
```
sudo passwd -S doe
```
To display information of all users
```
sudo passwd -Sa
```
To delete user’s password
```
sudo -d doe
```
</details>
<details>
  <summary>chage</summary>
  
To view the account aging information of user doe
```
chage -l doe
```
To set the last password change date to your specified date for user doe
```
chage -d 2025-12-31 doe
```
To set the date when the account should expire
```
chage -E 2025-12-31 doe
```
To remove expiration
```
sudo chage -E -1 doe
```
To specify the maximum number of days between password change
```
chage -M 90 doe
```
</details>
<details>
  <summary>chpasswd</summary>

update passwords in batch mode
```
sudo chpasswd
```
storing username and password in a file and give input to chpasswd
```
cat > password.txt
```
```
sudo chpasswd < password.txt
```
To apply encryption algorithm on password
```
sudo chpasswd -c SHA512
sudo chpasswd -c SHA256
sudo chpasswd --md5
```
</details>
<details>
  <summary>finger</summary>
  
To display information about system user and user doe
```
finger doe
```
To get idle status and login details of a user
```
finger -s doe
```
To show multiple users at once
```
finger doe alice john
```
</details>
<details>
  <summary>id</summary>
  
To print your own id without any options
```
id
```
To find a specific user doe id
```
id -u doe
```
To find out UID and all groups associated with a username
```
id doe
```
To find out all the groups a user doe belongs
```
id -nG doe
```
</details>
<details>
  <summary>who</summary>
  
To print who command output without options
```
who
```
To print the login names and total number of logged on users
```
who -q
```
To view the time of last system boot
```
who -b
```
To check the current runlevel
```
who -r
```
</details>
<details>
  <summary>whoami</summary>
  
To show the name of the currently logged-in user
```
whoami
```
</details>
<details>
  <summary>logname</summary>
  
To display user’s login name
```
logname
```
</details>
<details>
  <summary>last</summary>
  
To list of the most recent logins and logouts of users, as recorded in the /var/log/wtmp file
```
last
```
To list last five users logged in
```
last -5
```
To display the login and logout time including the dates
```
last -F
```
To display within a specific time period.(-s) since and (-t) until
```
last -s yesterday -t today
```
</details>
<details>
  <summary>w</summary>
  
To Show who is logged on and what they are doing
```
w
```
</details>

<details>
  <summary>users</summary>
  
To print the user names of users currently logged in to the current host
```
users
```
To Combine with wc to count logged-in users
```
users | wc -w
```
</details>
<details>
  <summary>chgrp</summary>
  
To Change group ownership of a file
```
sudo chgrp devops project.txt
```
To change a directory example_dir group ownership
```
sudo chgrp devops example_dir
```
To recursively change group ownership
```
sudo chgrp -R devops example_dir
```
</details>
<details>
  <summary>login</summary>
  
To log in to the system as user doe , preserves environment variables from the previous session
```
# login -p doe
```
To login to a domain
```
# login test.hashlabs.in
```
To Use with -f option (automatic login)
```
# login -f alice
```
</details>
<details>
  <summary>logout</summary>
  
To logout the user from the current session from logon shell
```
logout
```
</details>
<details>
  <summary>loginctl</summary>
  
To Show all sessions and attributes
```
loginctl -a
```
To display session configuration message
```
loginctl show-session
```
To list currently logged in users
```
loginctl list-users
```
</details>
<details>
  <summary>nologin</summary>
  
To Prevent a user from logging in
```
sudo usermod -s /sbin/nologin ftpuser
```
```
sudo usermod -s /sbin/nologin john
```
To check
```
grep john /etc/passwd
```
create a custom message file shown by nologin
```
echo "Access to this system is restricted." | sudo tee /etc/nologin.txt
```
</details>
<details>
  <summary>su</summary>
  
To Switch to the root user
```
su
```
su command to switch users without a password
```
# su - alice
```
To switch to root user
```
su -
```
To Use su with sudo command
```
sudo su - alice
```
</details>
<details>
  <summary>sudo</summary>
  
To run command as a root user
```
sudo apt update
```
To List user privileges with sudo
```
sudo -l
```
To add users to the sudoers file
```
sudo visudo
```
Edit a file that requires root privileges
```
sudo vim /etc/ssh/sshd_config
```
</details>
<details>
  <summary>sudoreplay</summary>
  
To List recorded sessions
```
sudo sudoreplay -l
```
To list sessions run by user your_user with a command containing the string vim
```
sudo sudoreplay -l user doe command vim
```
Default log directories:
```
/var/log/sudo-io
```
</details>
<details>
  <summary>setsid</summary>
  
To Run myscript.sh in the background.Even if you close the terminal, it keeps running because it’s in a separate session.
```
setsid myscript.sh &
```
Run a GUI app detached from the terminal, ex. Launches Gedit independently from the
terminal; closing the terminal won’t kill it.
```
setsid gedit &
```
</details>
<details>
  <summary>faillog</summary>
  
To Show all failed login attempts
```
sudo faillog
```
To display the faillog records for all the users
```
sudo faillog -a
```
To Show failed login info for a specific user doe
```
sudo faillog -u doe
```
To lock an account doe for 2 minute / 120 seconds after failed login
```
sudo faillog -l 60 -u doe
```
To set the maximum number of login failures for user doe
```
sudo faillog -m 5 -u doe
```
</details>
<details>
  <summary>chfn</summary>
  
To Change your own finger information interactively
```
chfn
```
To change the full name on the account from alice to doe
```
sudo chfn -f doe alice
```
To change the work phone number on the account doe
```
sudo chfn -w 9999988888 doe
```
</details>
<details>
  <summary>newusers</summary>
  
create users details in a file
```
sudo vim users.txt
```
```
alice:$6$abcd1234$xyz:1001:1001:Alice:/home/alice:/bin/bash
doe:$6$efgh5678$xyz:1002:1002:Doe:/home/doe:/bin/bash
```
```
sudo chmod 0600 users.txt
```
run the newusers command to add the users in the users.txt
```
sudo newusers users.txt
```
To check
```
cat /etc/passwd
```
</details>
<details>
  <summary>wall</summary>

To send a message on the terminals of all logged-in users
```
sudo wall "The system will be rebooted in 20 minutes."
```
```
sudo wall
The server will reboot in 15 minutes.
Please log out safely.
```
CTRL+D
To pipe the output of another command to wall
```
echo "The system will be rebooted in 20 minutes. save your work." | wall
```
</details>
<details>
  <summary>write</summary>
  
To write a message to user2 from user1
```
write user2
```
this is test message
^D
To pipe a message to write
```
echo "Hello from user1" | write user2
```
</details>
<details>
  <summary>mesg</summary>
 
To display the current write status of your terminal
``` 
mesg
```
To disallow write access to your terminal
```
mesg n
```
To allow write access to your terminal
```
mesg y
```
</details>
