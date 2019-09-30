# Instal·lació i configuració Apache i mòdul PHP

1. [REQUISITS DEL SISTEMA](#Requisits-del-servidor)
2. [INSTAL·LACIÓ SERVIDOR WEB APACHE](#install-apache)
3. [CONFIGURACIÓ /etc/hosts (DOMINIS)](#configuració-del-domini)
4. [INSTA·LACIÓ I CONFIGURACIÓ DE SERVIDOR SSH (ADMINISTRACIÓ REMOTA)](#administració-remota)
5. [INSTAL·LACIÓ PHP](#install-de-php)
6. [INSTAL·LACIÓ DE LA DOCUMENTACIÓ DEL PHP](#install-documentació-del-PHP)
7. [COMPROVACIONS](#comprovacions)

# Requisits del servidor

Cal destacar que m’he basat en els requeriments que proposa ubuntu en la seva documentació.

[https://help.ubuntu.com/community/Installation/SystemRequirements](https://help.ubuntu.com/community/Installation/SystemRequirements)

He decidit posar 2 GB de RAM, perquè es un kubuntu desktop que consumeix una mica més de recursos. Tema de HDD he decidit reservar 30 GB al S.O, ja que el requisit mínim son 25 GB. El tema bridge sens dubte m’he decidit per el Bridge, ja que documentaré i comprovaré que funciona des de el navegador de la maquina host.

![Requeriments](/img/1.png)

# Install Apache

Primer de tot hem de crear la maquina virtual, actualitzar-la i actualitzar els repositoris.

![Requeriments](/img/2.png)
![Requeriments](/img/3.png)

Un cop fet, l’actualització “obligàtoria”, descarreguem del repositori el packet d’apache2.

![Requeriments](/img/4.png)

Comprovem que el servei d'apache i l’escolta del port 80 està funcionant.

![Requeriments](/img/5.png)
![Requeriments](/img/6.png)

Quan ha acabat els passos previs, es hora de configurar el Firewall, com no anem molt sobrats de temps i no es una empresa. El deshabilitarem per evitar problemes.

![Requeriments](/img/7.png)

##### Fitxers importants 

Per començar veiem que crea un directori, per defecte, en el qual posarem els recursos, en la majoria de casos html, que retorni en cas de peticions. La ruta es /var/www/html

![Requeriments](/img/24.png)

En el nostre cas ens ha creat el seu html per defecte, que es el que veiem cada vegada que peticionem al nostre servidor. Ens posem en el directori que ha creat per la configuració d’apache2.

![Requeriments](/img/25.png)

Veiem que el primer fitxer que trobem es apache2.conf, aquest es el que conté la configuració general del servidor, i inclueix altres fitxers que estan guardats en altres directoris.

També destacar els arxius que es crean en /etc/apache2/sites-available, ja que aquest et permet configurar el teu/s virtual host/s.

![Requeriments](/img/26.png)

En el nostre cas, no tenim cap virtual host, per tant tenim el arxiu de configuració per el lloc per defecte.

També destacar els arxius que estan en /etc/apache2/sites-enabled/ ja que cada vegada que apache carregui la configuració, carregara els virtual hosts que permetem aquí.
 
En el directori /etc/apache2/mods-* contenim tots els mòduls disponibles i hablitats amb una estructura standar, el fitxer .load que conté els mòduls en si, i els .conf que guarden la configuració d’aquests mòduls.

![Requeriments](/img/27.png)

Per la part de logs, apache2 crea un directori /var/log/apache2/*.log en el qual podem consultar els logs.

![Requeriments](/img/28.png)

##### COMPROVACIÓ

Des de qualsevol dispositiu de la xarxa, amb un navegador, podem consultar que el servidor respon.
Comprovem l’IP del servidor.

![Requeriments](/img/8.png)

Posem la IP que volem comprovar en el navegador.

![Requeriments](/img/9.png)


# Configuració del domini

Si no volem instal·lar un servidor de DNS que resolgui els dominis, es pot fer una modificació en el fitxer de /etc/hosts. 

![Requeriments](/img/10.png)

Comprovem que resol cap al localhost.

![Requeriments](/img/11.png)

Afegim al fitxer /etc/hosts l’IP del company Isaac.

![Requeriments](/img/22.png)

Hem afegit el port ja que ell en el XAMPP ha configurat en el 8080.

![Requeriments](/img/23.png)

# Administració remota

Comencem la instal·lació des de els repositoris amb el mòdul de openssh-server

![Requeriments](/img/12.png)

Com en el exercici anterior hem deshabilitat el Firewall, no ens donarà problemes, sinó hauríem de crear la regla del Firewall que ens permet obrir el port 22. Comprovem que el servei i el port estant escoltant.

![Requeriments](/img/13.png)
![Requeriments](/img/14.png)

Un cop instal·lat, modificarem el fitxer /etc/ssh/sshd_config per poder habilitar el login des de el usuari root.

![Requeriments](/img/15.png)
![Requeriments](/img/16.png)

Un cop modificat el fitxer, reiniciem el servei de ssh.

![Requeriments](/img/17.png)

Un cop fetes les comprovacions prèvies, provarem a conectar desde un altre dispositiu de la xarxa, en el meu cas des de la maquina host.
Utilitzarem un software gratuït que s’anomena Putty. Deixo el link del instal·lador.

[https://www.putty.org/](https://www.putty.org/)

Comprovem quina IP té el servidor ssh per conectar-nos.

![Requeriments](/img/18.png)

Desde el client, facilitem la IP, el port i el tipus de connexió i obrim aquesta.

![Requeriments](/img/19.png)

El primer cop que entrem, com encara no tenim la clau del servidor, el client no te el fingerprint per poder comprobar si el equip remot, es realmente el equip al qual ens volem conectar, per tant ens demana si afegim aquest fingerprint al client.

![Requeriments](/img/20.png)

Un cop afegit el fingerprint, ens demanara les credencials. Posem el usuari root, en el meu cas i veiem que estem dintre del servidor apache i ssh.

![Requeriments](/img/21.png)

##### CONCLUSIÓ

La principal funció del SSH, es poder administrar i mantenir remotament els teus servidors, amb la ajuda o no d’internet, d’una manera molt segura, ja que utilitza una capa de seguretat que el seu antecessor Telnet no tenia. Es a dir, que ens permet connectar-nos des de qualsevol lloc del mon amb internet als nostres servidors d’una manera segura, així que si patim un man in the middle els paquets que veurà estaran encriptats.
S’utilitza en grans empreses o grans infraestructures, ja que et permet administrar sense estar físicament al lloc. També es pot utilitzar en petites empreses, ja que no has d’estar treballant en el CPD, sinó estas al teu lloc amb connexió i pots administrar sense problemes. Tema hosting, si tens una web allotjada a internet, encara que tinguis un panell de control, potser necessites fer alguna cosa que a través d’aquell panell no t’ho permeti.

# Install de PHP.

El servidor web apache2 esta implementat utilitzant una arquitectura en mòduls molt semblant al kernel de Linux.

Per consultar els mòduls compilats dins el codi de l'apache.

![Requeriments](/img/29.png)

Per instal·lar mòduls addicionals ho podem fer modificant fitxers de configuració, sense
necessitat de recompilar l'Apache.

Dos directoris importants dins /etc/apache2
* /etc/apache2/mods-available
* /etc/apache2/mods-enabled

Quan s'activa un mòdul es crea un enllaç simbòlic dels arxius de mods-available o mods-enabled.

Tot mòdul té dos fitxers de configuració.
* modul.load. (En temps de càrrega)
* modul.conf. (En temps de configuració)

Seguim les instruccions de la web d'Ubuntu.

[https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)


![Requeriments](/img/30.png)

Com ja el tenim instal·lat només haurem d'iniciar el servei de php i reiniar el d'Apache.

![Requeriments](/img/32.png)

Creem el arxiu de informació de PHP.

![Requeriments](/img/33.png)

Anem a comprovar que el PHP funciona correctament

![Requeriments](/img/34.png)

Creem un nou arxiu php a...

```bash
 /var/www/html
 ```

Aquesta és la carpeta per defecte a on buscarà obrir els arxius apache2

A continuació, executem la comanda:

```bash
nano /var/www/html/phpinfo.php
```

El contingut serà el següent
```html
<html>
<head>
		<title>PHPINFO</title>
</head>
<body>
		<?php
		echo phpinfo();
		?>
</body>
</html>
```

![Requeriments](/img/35.png)

Si ara carreguem aquest arxiu al navegador, ens mostrarà la informació de la nostra configuració. (Treu aquesta imatge i afegeix la teva al teu informe)

![Requeriments](/img/36.png)

Per afegir un àlies primer de tot haurem d’activar el mòdul d’apache2 amb

```bash
a2enmod alias
```

Per defecte ja hauria de venir activat!!!

![Requeriments](/img/37.png)

Un cop activat modificarem l’arxiu de configuració que serà on afegirem l'àlies

```bash
nano /etc/apache2/mod-enabled/alias.conf
```
 
Abans del tancament de l’etiqueta afegirem les línies de la imatge

![Requeriments](/img/38.png)

Guardarem l’arxiu i reiniciarem Apache.

![Requeriments](/img/39.png)

Accedim amb el navegador a (compte amb la última barra):

http://localhost/jose/

Caldria posar-hi un index.html a dins el directori /home/usuari/public_html/ i donar
permisos a tot plegat. Crear el nou arxiu i l’emplenar-ho amb un text simple

Creem un arxiu que ens mostrara el nostre alias, en la zona habilitada.

![Requeriments](/img/40.png)

Podem canviar l’usuari i grup propietaris amb les comandes CHOWN i CHGRP

![Requeriments](/img/41.png)

Amb aquest nou arxiu ja no es carregarà l’arbre d’arxiu del directori sinó aquest arxiu en el navegador

![Requeriments](/img/42.png)

Per tal de poder crear scripts i seguint el manual

[https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

Comprova en quin lloc del sistema de fitxers ha quedat instal·lat el mòdul de php. 
Pots utilitzar la comanda dpkg.

Comprovem on han quedat instal·lat els fitxers.

![Requeriments](/img/43.png)

# Install documentació del PHP

Per instal·lar la documentació primer de tot anem a la web oficial de php per descarregar-la.
https://www.php.net/docs.php

![Requeriments](/img/44.png)

Un cop descarregada la documentació la descomprimim en el directori /var/www/html i canviem el nom de la carpeta mare a doc/.

![Requeriments](/img/45.png)

# COMPROVACIONS
Hauries de poder-hi accedir fent http://localhost/doc/

![Requeriments](/img/46.png)

Un cop el tinguis instal·lat accedeix a la primera pàgina del tutorial de php i executa
l'exemple de "hola mon":
		http://ipservidor/doc/tutorial.firstpage.html

![Requeriments](/img/47.png)

Creem el arxiu helloworld.php en el nostre servidor apache.

![Requeriments](/img/48.png)

Comprovem que s’executa codi php en el nostre servidor. Amb el PHP instal·lat en el servidor printaria “Hola Mundo” en el navegador. 

![Requeriments](/img/49.png)

En el navegador, només veuríem el codi generat per el servidor, es a dir, que no es veuria el nostre codi php, ja que s’executa en el costat del servidor.

![Requeriments](/img/50.png)
