# Owncloud instalación
Aqui enseñaré como instalar el Owncloud mediante la terminal de Linux
## Instalar apache2, MySQL y librerías al contenedor
### 1. Actualización de la máquina virtual.

Para actualizar la máquina tendremos que poner el código ***sudo apt update*** en la terminal, darle al enter y esperar
![1](1.png)
Te pedira contraseña si entras por primera vez, escribe la contraseña de tu usuario, en mi caso "usuario" y le das a enter.
![2](2.png)

Después de actualizar la maquina le pondremos otro comando, el cual es: ***sudo apt upgrade*** y le daremos a enter.
![3](3.png)
Nos preguntará si queremos continuar, solo debemos escribir que si "s"
![4](4.png)

### 2. Instalar el servidor web 'apache2'.
Para instalar apache2 tendremos que poner ***sudo apt install -y apache2***
![6](6.png)
![7](7.png)

### 3. Instalación del servidor de bases de datos ***mysql-server***
Para instalar el servidor de base de datos debemos de poner ***sudo apt install -y mysql-server***
![8](8.png)

### 4. Instalación de librerías de 'php', lenguaje principal utilizado para aplicaciones.

Esto se hace con ***sudo apt install -y php libapache2-mod-php***
![10](10.png)
![11](11.png)

Ahora tenemos que poner el siguiente comando ***sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl***
![12](12.png)
![13](13.png)

### 5. Reiniciar el servidor
***sudo systemctl restart apache2***
![14](14.png)

## Como configurar MySQL

Como acceder a la consola de MySQL
Ponemos el siguiente comando ***sudo mysql***

![15](15.png)

A continuación se deben poner comandos para crear la base de datos, un usuario, contraseña y otorgar permisos

***CREATE DATABASE bbdd;***
***CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';***
***GRANT ALL ON bbdd. to 'usuario'@'localhost'***
![16](16.png)

#### Salir de la base de datos
Como se muestra en la anterior captura, salgo de la base de datos mediante el comando
***exit***

## Como instalar la versión 7.4 de PHP Ubuntu 24.04
### 1.Como instalar los requisitos previos de PPA.
Para instalar los requisitos previos de PPA debemos de poner ***sudo apt install software-properties-common -y***

![17](17.png)

### 2.Descargar herramientas necesarias para trabajar con los archivos de paquetes personales (PPA).
Debemos poner el siguiente comando ***LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y***

![18](18.png)
![19](19.png)
### 3.Actualizar
Utilizaremos el comando que usamos al principio, ***sudo apt update***

![20](20.png)

### 4.Instalar las librerías de PHP versión 7.4

Primero debemos de poner el siguiente comando ***sudo apt install php7.4 -y***

![21](21.png)

Ahora continuar con ***sudo apt install -y php libapache2-mod-php7.4***

![22](22.png)

Continuamos con el ultimo comando ***sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl***

![23](23.png)

### 5.Seleccionar la versión de PHP.

En este paso se debe seleccionar una versión de PHP, la 7.4

Para empezar debemos escribir ***sudo update-alternatives --config php***

![24](24.png)

A continuación pondremos al número ***2***

![25](25.png)

### 6.Activar los módulos de apache2 necesarios
Despues de haber realizado el paso anterior debemos de poner ***sudo a2enmod proxy_fcgi setenvif***

![26](26.png)

Y a continuación ***sudo a2enconf php7.4-fpm***

![27](27.png)

### 7.Reiniciar apache2

Con ***sudo service apache2 restart***

![28](28.png)

## Instalar OwnCloud

[Descargar Owncloud aqui](https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip) 

## Descargar ficheros de la appweb

### 1.Cp al .zip del OwnCloud recien descargado/2. Acceder al directorio /var/www/html

Usaremos el siguiente comando ***sudo cp ~/Descargas/owncloud-complete-20240724.zip /var/www/html*** este comando varia dependiendo de la ubicación del archivo
Despues de escribir el comando anterior accederemos a /var/www/html con ***cd /var/www/html***

![29](29.png)

### 3.Descomprimir el archivo

Lo haremos con ***sudo unzip owncloud-complete-20240724.zip*** en mi caso no pude encontrar donde puse el comando por sonrecarga de texto pero lo pongo al final para saber que poner

![30](30.png)

### 4.Copiar los ficheros en la carpeta /var/www/html

Los copiaremos con ***sudo cp -R owncloud/. /var/www/html***

![31](31.png)

### 5.Eliminar la carpeta creada

Lo hacemos con ***sudo rm -rf owncloud/***

![32](32.png)

### 6.Eliminar index.html del apache2
Lo hacemos con el comando ***sudo rm -rf /var/www/html/index.html***

![33](33.png)

### 7.Permisos de  aplicaciones web

Primero vamos a la carpeta correcta con ***cd /var/www/html***
Y ahora ponemos ***sudo chmod -R 775 .***

![34](34.png)

Y finalmente pondremos ***sudo chown -R usuario:www-data .***

![35](35.png)

## Acceder a OwnCloud

Primero debemos acceder a la pagina de local host con el siguiente enlace [Local Host](http://localhost/) 

Si todo esta correcto deberia salir esto

![36](36.png)

La información que debemos poner es esta:

usuario: usuario
contraseña: password
base de datos: bbdd
dominio: localhost

Una vez puesto nos saldrá esto

![37](37.png)

Ahora toca configurar el OwnCloud, explicado en: https://github.com/AdriFroste/owncloud.alr/blob/main/config%20owncloud
