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


järgmisena sisestasin sources.listi 
