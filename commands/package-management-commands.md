<details>
  <summary>apt</summary>

To update the local package index with the latest information from the repositories
```
sudo apt update
```
To upgrade all installed packages to the latest available versions
```
sudo apt upgrade
```
To upgrade the system including removing old packages and handling dependencies
```
sudo apt full-upgrade
```
To install a specific package
```
sudo apt install vsftpd
```
```
sudo apt install curl
```
To install multiple packages at once
```
sudo apt install vsftpd curl vim
```
To remove an installed package but keep its configuration files
```
sudo apt remove vsftpd
```
To completely remove a package (including configuration files)
```
sudo apt purge curl
```
```
sudo apt purge vsftpd
```
To search for a package in the repositories
```
sudo apt search nginx
```
To show detailed information about a specific package
```
apt show apache2
```
To list all installed packages on the system
```
apt list --installed
```
Cleaning Up Unused Packages
To remove packages that were installed as dependencies but are no longer required (because no installed package depends on them)
```
sudo apt autoremove
```
Cleaning the Package Cache
To clear the local repository of downloaded package files (to free up space)
```
sudo apt clean
```
To remove only outdated package files
```
sudo apt autoclean
```
To clean up orphaned packages that were automatically installed as dependencies and are no longer required
```
sudo apt-get autoremove --purge
```
To fix broken packages (incomplete installs, unmet dependencies)
```
sudo apt --fix-broken install
```
To list all the packages that have updates available
```
apt list --upgradable
```
To upgrade a specific package
```
sudo apt install --only-upgrade curl
```
To view the dependencies of a package
```
apt depends curl
```
To install a specific version of a package curl
```
sudo apt install 
`
```
If a package is missing dependencies, you can try installing them manually with
```
sudo apt install -f
```
To reinstall a package
```
sudo apt install --reinstall curl
```
To install package.deb using apt
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
```
sudo apt install ./google-chrome-stable_current_amd64.deb
```
To Find Help for apt
```
sudo apt help
```
To Verify a Package for any Broken Dependencies
```
sudo apt check apache2
```
To simulate an action (dry-run)
```
sudo apt install --simulate nginx
```
To simulate removal
```
sudo apt remove --simulate nginx
```
To download a .deb package file without installing it
```
sudo apt download <package-name>
sudo apt download curl
```
To show a list of all repositories (apt sources), their priorities, and their origins (e.g., Ubuntu archive, PPA, etc.)
```
apt policy
```
To upgrade your entire distribution to a new version
```
apt update
cat /etc/os-release
sudo apt upgrade
sudo apt dist-upgrade
sudo apt autoremove
sudo apt install update-manager-core
vim /etc/update-manager/release-upgrades
Prompt=lts
reboot
sudo do-release-upgrade
cat /etc/os-release
```
</details>
<details>
  <summary>aptitude</summary>
 
To install aptitude
```
sudo apt install aptitude
```
To update the package list
```
sudo aptitude update
```
To upgrade all the installed packages to their latest versions
```
sudo aptitude upgrade
```
To perform an upgrade and also handles changing dependencies (removing obsolete packages if necessary)
```
sudo aptitude full-upgrade
```
To install a package
```
sudo aptitude install vim
```
To install a specific version of a package
```
sudo aptitude install curl=7.68.0-1ubuntu2.6
```
To remove a package
```
sudo aptitude remove curl
```
To remove a package along with its configuration files
```
sudo aptitude purge nginx
```
To search for a package
```
aptitude search vsftpd
```
To show detailed information about a package
```
aptitude show vsftpd
```
To search for a package and filter by category
```
aptitude search ~i
```
To search for a package that is not installed
```
aptitude search ~n
```
To mark a package to hold (prevent it from being upgraded)
```
sudo aptitude hold nginx
```
To unmark a held package
```
sudo aptitude unhold nginx
```
To clean the package cache
```
sudo aptitude clean
```
To fix broken packages
```
sudo aptitude install -f
```
To list upgradable packages
```
aptitude search '~U'
```
To view package dependencies
```
aptitude why <package-name>
```
```
aptitude why apache2
```
To make interactive interface
```
sudo aptitude
```
</details>
<details>
  <summary>add-apt-repository</summary>
  
To add a repository
```
sudo add-apt-repository ppa:PPA_REPOSITORY_NAME/PPA
```
```
sudo add-apt-repository ppa:libreoffice/ppa
```
```
sudo apt update
```
To list all repositories
```
sudo apt policy
```
To add a repository via URL
```
sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ focal main universe"
```
```
sudo apt update
```
To remove PPA repository
```
sudo add-apt-repository --remove ppa:PPA_REPOSITORY_NAME/PPA
```
```
sudo add-apt-repository --remove ppa:libreoffice/ppa
```
```
sudo apt update
```
</details>
<details>
  <summary>dpkg</summary>
  
To install a .deb package
```
sudo dpkg -i package.deb
```
To remove an installed package (keep config files)
```
sudo dpkg -r package-name
```
To remove an installed package (remove config files)
```
sudo dpkg -P package-name
```
or
```
sudo dpkg --purge package-name
```
To list all installed packages
```
dpkg -l
```
To check if a package is installed
```
dpkg -s curl
```
To list files installed by a package
```
dpkg -L curl
```
To print information about a .deb package
```
dpkg -I package.deb
```
To verify installed files of a package
```
dpkg -V package-name
```
To view the content of a package
```
sudo dpkg -c package_name.deb
```
check the location of packages installed
```
sudo dpkg -L package_name.deb
```
</details>
