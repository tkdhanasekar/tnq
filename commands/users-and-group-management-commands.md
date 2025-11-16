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

