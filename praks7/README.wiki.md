# DOKUWIKI

dokuwiki paigaldamiseks tegin enne apt update.

seejärel tegin otsisin dokuwiki lehelt https://download.dokuwiki.org/get?id=8a269cc015a64b40e4c918699f1e1142 uusima versiooni download lingi.

antud lingiga tegin wget ning pakkisin tar-xzvf käsuga selle lahti.
Tekkinud kausta tõstsin /var/www/html kausta ja määrasin antud kaustale grupiks/omanikuks www-data käskudega:
```
chown -R www-data /var/www/html/dokuwiki
chgrp -R www-data /var/www/html/dokuwiki
```

Touch käsuga tegin ka wiki/data kausta sisse changes.log faili.

lehele minemiseks sisestasin aadressi ribale 192.23.13.49/dokuwiki ning seejärel avanes wiki avaleht. Paremal tekstivälja kõrval oli edit this page ning muutsin lehte.

erinevad lehe muutmise failid asuvad /var/www/html/dokuwiki/data/pages kaustas.

sinna samasse kausta saab teha ka erinevate lehtede .txt failid, mida saab linkida erinevatele lehtedele kasutades [[2ndpage]] kujul süntaksi (2 kandilist sulgu, lehe faili nimi ilma laiendita, 2 kandilist sulgu).

kuskile veebilehele suunamiseks tuleb sisestada süntaks kujul näiteks:
```
[[http://www.google.com|This Link points to google]]
```

see tekitab wiki lehele lause "This Link points to google", millele vajutades lähed google avalehele. 


pealkirjade loomiseks tuleb teha
```
==== kolmas tase ====
=== neljas ===
== viies ==
``` 

piltide lisamiseks tuleb kasutada loogelisi sulgusid {{}}.
