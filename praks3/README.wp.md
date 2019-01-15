# PHP ja MYSQL moodulite paigaldus.

# moodulite paigaldamine
php moodulite paigaldamiseks lisasin /etc/apt/sources.list faili read: 
```
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```
peale seda salvestasin faili ja tegin apt-update, peale mida sain teha php7.0-cli php7.0-curl php7.0-dev php7.0-zip 
php7.0-fpm php7.0-gd   php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-mbstring php7.0-opcache

selleks, et paigaldada veebiserveriks vajalikud php paketid. 

# mysql paigaldamine

peale php pakettide paigaldamist läksin /tmp kausta ning laadisin wget https://dev.mysql.com/get/mysql-apt-config_0.8.9-1_all.deb
käsuga alla mysql configu.

Käsuga dpkg -i mysql-apt-config_0.8.9-1_all.deb pakkisin selle lahti ning kohe tuli ka configuration, kus sai valida
versiooni jne. versiooniks panin 5.6

Peale seda tegin jälle apt-update ja apt-get install mysql-community-server, millega määrasin mysql root kontole parooli jne.


mysqli käsureal sisselogimiseks ilma paroolita tegin root kasutaja kodukausta faili .my.cnf kuhu sisse panin
```
[mysql]
user=root
password=qwerty
```

# phpmyadmin install

apt install phpmyadmin käsuga paigaldasin myphpadmini lehe. Paroolideks määrasin qwerty

järgmisena tegin nano /etc/apache2/apache2.conf ja lisasin rea Include /etc/phpmyadmin/apache.conf ja tegin
systemctl restart apache2 käsuga apache teenusele restarti. Järgmisena läksin phpmyadmin lehele sisestades 172.23.13.49/phpmyadmin ja logisin
sisse kontoga root ja parooliga qwerty



# php lehe tegemine

algselt tegin index.php faili, kuhu panin algse lehe. Antud fail asub praks3 kaustas

php info kuvamiseks tegin /var/www/html kausta faili nimega test.php

faili sisestasin rea
```
<?php phpinfo(); ?>
```
pilt on saadaval praks3 kaustas .png failina




kasutajale oma lehe saamiseks tegin public_html kausta test.php faili, kuhu sisestasin tavalise teksti ning php käsuks panin 
```
<?php echo '<p> Kasutaja enda leht </p>'; ?>
```

kuna apache-l on defaultist keelatud php moodulid siis muutsin /etc/apache2/mods-enabled/php7.0.conf failis userdirmodule read commentiga ära.


kõik vajaminevad failid on olemas praks3 kaustas


# lehele https paigaldamine

algselt tegin apt update ja peale seda apt upgrade openssl

järgmisena a2enmod ssl ja a2ensite default-ssl, peale mida tegin apachele reload

järgmisena tegin /etc/apache2 kausta sisse ssl kausta.

peale seda käivitasin käsu openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt ja täitsin vajalikud väljad.

seejärel tegin nano /etc/apache2/sites-enabled/default-ssl.conf ja muutsin read 
```
ServerName vsh-rando:443
SSLCertificateFile /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```

peale mida tegin apachele reload ja peale seda openssl s_client -connect 172.23.13.49:443
ning läksin brauseris lehele https://172.23.13.49

pilt on lisatud kausta


# wordpress paigaldamine

tegin mysql andmebaasi ja kasutaja ning määrasin õigused 
```
mysql> CREATE DATABASE wpdatabase;
mysql> CREATE USER wpuser@localhost IDENTIFIED BY ‘wppass’;
mysql> GRANT ALL PRIVILEGES ON wpdatabase.* TO wpuser@localhost; 
mysql> FLUSH PRIVILEGES;
mysql> exit
```
seejärel tegin apache ja mysql teenustele restarti.

peale seda installisin ka zip käsu tehes apt install zip

peale seda laadisin alla wordpressi uusima versiooni
```
cd /tmp
wget -c http://wordpress.org/latest.zip
unzip -q latest.zip -d /var/www/html/
```


seejärel määrasin õigused ja tegin vajalikud kaustad jne

```
chown -R www-data.www-data /var/www/html/wordpress
chmod -R 755 /var/www/html/wordpress
mkdir -p /var/www/html/wordpress/wp-content/uploads
chown -R www-data.www-data /var/www/html/wordpress/wp-content/uploads
```

´´´
cd /var/www/html/wordpress/
cp wp-config-sample.php wp-config.php
nano wp-config.php
´´´


seal failis muutsin ära wp database, useri ja passwordi.

userfriendly lehe jaoks muutsin settings ja permalinks alt custrom structure /%postname%/ ja salvestasin


muudetud fail ja pilt on lisatud kausta
