# WEBSERVER LINUX
- Si installa la macchina virtuale (Ubuntu Server)
- Si accede con l'account amministratore
- SI installa apache2
>sudo apt update
>sudo apt install apache2
- Verifca dello stato
>sudo systemctl status apache2
- Si configura l'indirzzo ip statico
> sudo nano /etc/netplan/00-netcfg.yaml
>```bash
> network:
> version: 2
> renderer: networkd
> ethernets:
> enp0s3:
>     dhcp4: no
>     addresses: [172.16.29.x/24]
>     gateway4: 172.16.29.1
>     nameservers:
>       addresses: [8.8.8.8,8.8.4.4]

>  sudo netplan apply
oppure
> sudo netplan try

- In seguito si vanno a creare delle sottocartelle che conterranno i vari siti e si crea un utente per ciascuno di essi
> cd /var/www
> mkdir **nomesito**
> cd **nomesito**
> mkdir log
> mkdir html
- Si inseriscono le pagine html
- Si crea un utente per gestire il sito
> sudo useradd -s /bin/bash -d /var/www/sitoa -m usersitoa
> sudo passwd usersitoa
- Si creano o copiano i file di configurazione per il nuovo sito
> sudo  cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/sito.conf
> sudo  nano /etc/apache2/sites-available/sito.conf
>>```bash
>>  <VirtualHost *:80>
>>      ServerAdmin webmaster@localhost
>>    DocumentRoot /var/www/html
>>      ErrorLog ${APACHE_LOG_DIR}/error.log
>>      CustomLog ${APACHE_LOG_DIR}/access.log combined
>></VirtualHost>
> sudo a2ensite example.com.conf
> sudo systemctl restart apache2
- Eventualmente si aggiorna la lista degli host
> sudo  nano /etc/hosts
>>bash
>>127.0.0.1   localhost
>>ip sito.com yfutfg
