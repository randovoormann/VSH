# andmebaasi server

andmebaasi serverile paigaldasin mariadb-server ning käivitasin mysql installationi. käsuga
```
apt install mariadb-server

mysql_secure_installation
```

mysql installationis panin kõigele peale parooli vahetuse yes.



Järgmisena muutsin /etc/mysql/my.cnf failis bind-address rea ära ning sisestasin
andmebaasi serveri ip, milleks oli 10.0.2.6

peale seda tegin mysql teenusele restarti.

seejärel sisenesin mysqli sisse ning sisestasin käsud

```

CREATE DATABASE wordpress;
CREATE USER 'WPuser'@'localhost' IDENTIFIED BY 'qwerty';
GRANT ALL PRIVILEGES ON wordpress.* TO 'WPuser'@'localhost';
CREATE USER 'WPuser'@'10.0.2.5' IDENTIFIED BY 'qwerty';
GRANT ALL PRIVILEGES ON wordpress.* TO 'WPuser'@'10.0.2.5';
exit

```


# wordpressi server

Selle paigaldamiseks tegin apt update ja paigaldasin apache2 ning mariadb-client ja php-mysql.
Samuti laadisin alla ka zip käsu

järgmisena sisestasin sources.listi 

```
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all

```

ning tegin apt install php7.0-*

peale seda tegin service apache2 reload.

järgmisena läksin /tmp kausta ning laadisin alla wordpressi ja pakkisin selle lahti käskudega

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
```
cd /var/www/html/wordpress/
cp wp-config-sample.php wp-config.php
nano wp-config.php
```

wp-config.php failis muutsin ära useri, passwordi, database name ja ka hostname. hostname kohale panin 10.0.2.6

# klient

kliendi arvutile paigaldasin ubuntu 16.04 ja määrasin sellele 4GB RAM ja 10GB ketast.
