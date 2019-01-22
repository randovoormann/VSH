# DOKUWIKI

dokuwiki paigaldamiseks tegin enne apt update.

seejärel tegin otsisin dokuwiki lehelt https://download.dokuwiki.org/get?id=8a269cc015a64b40e4c918699f1e1142 uusima versiooni download lingi.

antud lingiga tegin wget ning pakkisin tar-xzvf käsuga selle lahti.
Tekkinud kausta tõstsin /var/www/html kausta ja määrasin antud kaustale grupiks/omanikuks www-data

Touch käsuga tegin ka wiki/data kausta sisse changes.log faili.

lehele minemiseks sisestasin aadressi ribale 192.23.13.49/dokuwiki ning seejärel avanes wiki avaleht. Paremal tekstivälja kõrval oli edit this page ning muutsin lehte.
