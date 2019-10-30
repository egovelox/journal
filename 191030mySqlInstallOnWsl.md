# Install mySQL on WSL Debian
La commande `sudo apt install mysql-server` ne pourra fonctionner avant d'avoir configurer les dépôts spécifiques SQL.
En outre, la version mySQL 8.0 passe à l'installation, mais impossible ensuite de lancer "sudo service mysql start" > mysql service not recognized.
On installe donc la version mysql-server-5.7

### Optionnel: Connaître la version de l'OS linux
`cat /etc/os-release`

### Mettre à jour

```
sudo apt update

sudo apt upgrade
```
### Install wget
`sudo apt install wget `

### Configure mySQL PPA

```
wget https://repo.mysql.com/mysql-apt-config_0.8.13-1_all.deb
sudo apt install lsb-release gnupg
sudo dpkg -i mysql-apt-config_0.8.13-1_all.deb
sudo apt update
```

### In case you want to change config
```
sudo dpkg-reconfigure mysql-apt-config

```
### Install
```
sudo apt install mysql-server

```
### Start
```
sudo service mysql start
mysql -u root -p          // will ask for your password

```

### (optional)
Can't recommend enough to run services like mysql via docker for windows

apt, service, comptes d'utilisateur et autorisations pour WSL
