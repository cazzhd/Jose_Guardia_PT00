# Instal·lació i configuració Apache i mòdul PHP

1. [REQUISITS DEL SISTEMA](https://github.com/joseluisguardia/migrationToO365/tree/master/introduction)
2. [INSTAL·LACIÓ SERVIDOR WEB APACHE](https://github.com/joseluisguardia/migrationToO365/tree/master/desenvolupament)
3. [CONFIGURACIÓ /etc/hosts (DOMINIS)](https://github.com/joseluisguardia/migrationToO365/tree/master/conclusio)
4. [INSTA·LACIÓ I CONFIGURACIÓ DE SERVIDOR SSH (ADMINISTRACIÓ REMOTA)](https://github.com/joseluisguardia/migrationToO365/tree/master/webgrafia)
5. [INSTAL·LACIÓ PHP](https://github.com/joseluisguardia/migrationToO365/tree/master/annexos)
6. [INSTAL·LACIÓ DE LA DOCUMENTACIÓ DEL PHP](https://github.com/joseluisguardia/migrationToO365/tree/master/agraiments)
7. [COMPROVACIONS](https://github.com/joseluisguardia/migrationToO365/tree/master/agraiments)

# Requisits del servidor

Cal destacar que m’he basat en els requeriments que proposa ubuntu en la seva documentació.

[https://help.ubuntu.com/community/Installation/SystemRequirements](https://help.ubuntu.com/community/Installation/SystemRequirements)

He decidit posar 2 GB de RAM, perquè es un kubuntu desktop que consumeix una mica més de recursos. Tema de HDD he decidit reservar 30 GB al S.O, ja que el requisit mínim son 25 GB. El tema bridge sens dubte m’he decidit per el Bridge, ja que documentaré i comprovaré que funciona des de el navegador de la maquina host.

![Requeriments](/img/1.png)

# Insta·lació del servidor web (Apache)

Primer de tot hem de crear la maquina virtual, actualitzar-la i actualitzar els repositoris.

![Requeriments](/img/2.png)
![Requeriments](/img/3.png)

Un cop fet, l’actualització “obligàtoria”, descarreguem del repositori el packet d’apache2.

![Requeriments](/img/4.png)

Comprovem que el servei d'apache i l’escolta del port 80 està funcionant.

![Requeriments](/img/5.png)
![Requeriments](/img/6.png)




