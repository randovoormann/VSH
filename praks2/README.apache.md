Paigaldada oli vaja apache2, enne mida tegin ära apt update. Peale seda paigaldasin apache veebiserveri käsuga apt install apache2. 

Seejärel tühjendasin /var/www/html/index.html faili. Selleks tegin touch käsuga tühja faili ja kopeerisin index.html faili asemele.

index.html fail asub arvutis tegelikult /var/www/html kaustas


tavakasutajale avaliku kausta tegemiseks kasutasin käsku mkdir /home/it/public_html.
seejärel linkisin selle /var/www kaustaga kasutades käsku ln -s /home/it/public_html/ /var/www
peale seda lubasin kasutaja kaustad käsuga a2enmod userdir ning tegin apache2 teenusele restarti. 
