# practica_LAMP

# 1. Instalación de phpMyAdmin.

## 1.1 Instalación de composer.

1. Primero debemos de actualizar los paquetes del server e instalar los complementos necesarios:

* sudo apt update
* sudo apt install wget php-cli php-zip unzip

2. Debemos descargar composer de la pagina web oficial:

* php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

3. Usaremos el siguiente wget para descargar desde la pagina de github el script del compositor:

* HASH="$(wget -q -O - https://composer.github.io/installer.sig)"

Verificamos la instalación: **php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"**

4. Instalar composer en el directorio local: 

* sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

5. Verificamos la instalación ejecutando el composer.

## 1.2 Instalación de phpmyadmin:

1. instalamos phpmyadmin desde el siguiente directorio:

* sudo apt install phpmyadmin php-mbstring php-gettext

El proceso de instalación agrega el archivo de configuración phpMyAdmin Apache en el directorio / etc / apache2 / conf-enabled /, donde se lee automáticamente. Lo que debes hacer es habilitar la extension PHP de mbstring, se modifica de la siguiente manera:

* sudo phpenmod mbstring

Una vez hecho esto, reiniciamos el servicio de apache:

* sudo systemctl restart apache2

2. Ajustar el logging para usuarios y los privilegios:

Para iniciar sesion en mysql como usuario root debemos cambiar el metido de autenticacion de auth_socket a mysql_native_password.

Esto debemos hacerlos desde el propio terminal de mysql:

* sudo mysql

Usaremos ALTER USER para autentificarnos con una contraseña:

* ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

3. Entrar en phpmyadmin: 

* localhost/phpmyadmin



# 2.Instalación de admminer.

1. Crear el directorio para adminer:

* sudo mkdir /usr/share/adminer

2. Instalación de adminer desde la pagina oficial:

* sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/latest.php

3. Con el comando ln podremos crear un enlace 















