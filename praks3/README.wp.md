# PHP ja MYSQL moodulite paigaldus.

php moodulite paigaldamiseks lisasin /etc/apt/sources.list faili read: 
```
deb http://packages.dotdeb.org jessie all
deb-src http://packages.dotdeb.org jessie all
```
peale seda salvestasin faili ja tegin apt-update, peale mida sain teha php7.0-cli php7.0-curl php7.0-dev php7.0-zip php7.0-fpm php7.0-gd php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-mbstring php7.0-opcache

selleks, et paigaldada veebiserveriks vajalikud php paketid. 

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

apt install phpmyadmin käsuga paigaldasin myphpadmini lehe. Paroolideks määrasin qwerty

php info kuvamiseks tegin /var/www/html kausta faili nimega test.php

faili sisestasin rea
```
<?php phpinfo(); ?>
```



järgmisena tegin nano /etc/apache2/apache2.conf ja lisasin rea Include /etc/phpmyadmin/apache.conf ja tegin
systemctl restart apache2 käsuga apache teenusele restarti. Järgmisena läksin phpmyadmin lehele sisestades 172.23.13.49/phpmyadmin ja logisin
sisse kontoga root ja parooliga qwerty
