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

