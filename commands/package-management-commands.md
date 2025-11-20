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
  <summary>apt-mark</summary>
  
Prevent curl from being upgraded (optional)
```
sudo apt-mark hold curl
```
To undo the hold
```
sudo apt-mark unhold curl
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
<details>
  <summary>dpkg-query</summary>

To list all installed packages
```
dpkg-query -l
```
To search for a package by name
```
dpkg-query -l '*python3*'
```
To show detailed information about an installed package
```
dpkg-query -s bash
```
To show the files installed by a package
```
dpkg-query -L bash
```
To find which package a file belongs to
```
dpkg-query -S /bin/ls
```
To format the output (package + version)
```
dpkg-query -W -f='${Package} ${Version}\n'
```
To show package, architecture, and description
```
dpkg-query -W -f='${Package}\t${Architecture}\t${Description}\n'
```
To list only package names
```
dpkg-query -W -f='${Package}\n'
```
To show the installed version of a package
```
dpkg-query -W -f='${Version}\n' openssl
```
To check if a package is installed
```
dpkg-query -W -f='${Status}\n' curl
```
To show removed-but-not-purged packages
```
dpkg-query -W -f='${Package} ${db:Status-Abbrev}\n' | grep 'rc'
```
</details>
<details>
  <summary>dpkg-deb</summary>
  
To show information about a .deb package
```
dpkg-deb --info package.deb
```
To list files inside a .deb
```
dpkg-deb --contents package.deb
```
To extract a .deb package to a directory
```
dpkg-deb --extract package.deb output-dir/
```
To extract control files only it is useful for editing metadata.
```
dpkg-deb --control package.deb control-dir/
```
To show package size info
```
dpkg-deb -f package.deb Installed-Size
```
To compare two .deb packages
```
diff <(dpkg-deb --contents pkg1.deb) <(dpkg-deb --contents pkg2.deb)
```
</details>
<details>
  <summary>dpkg-reconfigure</summary>
  
To reconfigure a package interactively
```
sudo dpkg-reconfigure tzdata
```
To reconfigure a package non-interactively (with default settings)
```
sudo dpkg-reconfigure -f noninteractive package-name
```
```
sudo dpkg-reconfigure -f readline debconf
```
To reconfigure keyboard layout
```
sudo dpkg-reconfigure keyboard-configuration
```
To reconfigure locales
```
sudo dpkg-reconfigure locales
```
To reconfigure MySQL/MariaDB root password
```
sudo dpkg-reconfigure mysql-server
```
Batch reconfigure multiple packages
```
sudo dpkg-reconfigure -f noninteractive tzdata locales
```
</details>
<details>
  <summary>pip/pip3</summary>
  
To install a package
```
pip install requests
```
To install a specific version
```
pip install requests==2.31.0
```
To upgrade a package
```
pip install --upgrade requests
```
To uninstall a package
```
pip uninstall requests
```
To list installed packages
```
pip list
```
To show detailed info about a package
```
pip show requests
```
To check outdated packages
```
pip list --outdated
```
To install packages from a requirements file
```
vim requirements.txt
```
```
numpy
botocore
```
````
pip install -r requirements.txt
```
To install a package for the current user only
```
pip install --user requests
```
To install from a Git repository
```
pip install git+https://github.com/psf/requests.git
```
To install a package with extra dependencies
```
pip install package_name[extra1,extra2,...]
```
Suppose we want to install requests with its optional security extras
```
pip install requests[security]
```
To specify multiple extras separated by commas
```
pip install requests[security,socks]
```
To upgrade pip itself
```
pip install --upgrade pip
```
To print version of pip3
```
pip3 --version
```
To list packages that don’t come pre-installed with Python
```
pip3 freeze
```
To check that installed packages are compatible
```
pip3 check
```
</details>
<deatils>
  <summary>update-alternatives</summary>

To configure update-alternatives for python versions
```
sudo apt update
sudo apt install -y software-properties-common build-essential wget
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install -y python3.10 python3.10-venv python3.10-dev python3.10-distutils python3.12-venv
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 2
sudo update-alternatives --config python3

python3.10 -m venv myenv3.10
source myenv3.10/bin/activate
python3 --version
deactivate

python3.12 -m venv myenv3.12
source myenv3.12/bin/activate
python3 --version
deactivate
```
To list all alternatives for python
```
update-alternatives --list python3
```
To show current choice and configuration
```
update-alternatives --display python3
```
Configure interactively (choose manually)
```
update-alternatives --config python3
```
Set an alternative manually
```
sudo update-alternatives --set java /usr/lib/jvm/java-11-openjdk/bin/java
```
Add a new alternative
```
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 50
sudo update-alternatives --install /usr/bin/editor editor /usr/bin/nano 40
```
Remove an alternative
```
sudo update-alternatives --remove editor /usr/bin/nano
```
Check the master link’s status
```
update-alternatives --query python3
```
Automatic mode
```
sudo update-alternatives --auto python3
```
To configure editor
```
sudo update-alternatives --config editor
```
</details>

