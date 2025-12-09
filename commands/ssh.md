To install ssh packages
```
sudo apt install openssh-server openssh-client
```
## To create ssh keys
To Generate a default RSA key (interactive)
```
ssh-keygen
```
To Generate a 4096-bit RSA key
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
To generate a 2048-bit RSA key
```
ssh-keygen -t rsa -b 2048 -C "your_email@example.com"
```
To generate a 1024-bit RSA key
```
ssh-keygen -t rsa -b 1024 -C "your_email@example.com"
```
Generate an Ed25519 key (recommended for most uses)
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
To generate a key without a passphrase
```
ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519
```
For the first time login to remote server with password and create a user
```
ssh root@remote_server_ip
```
update the system
```
apt update
```
set the hostname
```
hostnamectl set-hostname remote_server
```
```
exec bash
```
create a user and give sudo access
```
adduser user_name
```
```
usermod -aG sudo user_name
```
## copy the ssh public key to remote server from your local machine
```
ssh-copy-id -i ~/.ssh/ssh_key.pub user_name@remote_server_ip
```
Login
```
ssh user_name@remote_server_ip
```
## Now disable root login , enable publickey authentication , custom password , disable password authentication
```
sudo vim /etc/ssh/sshd_config
```
find these parameters and uncomment and change accordingly
```
Port 2222

PermitRootLogin no

PubkeyAuthentication yes

PasswordAuthentication no
```
save and exit

## disable ssh.socket
for ubuntu 22.10 or later version sshd might be using socket-based activation. In this case we need to disable ssh.socket 
and enable ssh.service for sshd_config file to take full effect 
```
sudo systemctl disable --now ssh.socket
```
```
sudo systemctl enable --now ssh.service
```
```
sudo systemctl restart ssh
```
check for syntax errors in the config file
```
sudo sshd -t
```
check with netstat or ss tool for ssh mapped port number
```
netstat -tulpn | grep ssh
```
or
```
ss -tulpn | grep ssh
```
