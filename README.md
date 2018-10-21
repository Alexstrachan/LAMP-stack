# practica_LAMP



# 0.Instalación de la pila LAMP.


## 0.1 Instalación de Apache2:

* sudo apt install apache 2

## 0.2 Instalación de MySQL Server:

* sudo apt install mysql-server mysql-client php-mysql

## 0.3 Instalación de PHP:

* sudo apt install php libapache2-mod-php php-mcrypt php-mysql

Crear y modificar info.php:

Crear "info.php" dentro del directorio "/var/www/html" :

* sudo nano info.php

Ahora debemos de introducir lo siguiente:

<?php

phpinfo();

?>

Consultamos en la ruta: "localhost/info.php"


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

3. Con el comando ln podremos crear un enlace entre los siguientes directorios:

* sudo ln -s /usr/share/adminer/latest.php /usr/share/adminer/adminer.php

4. Con el comando "echo" haremos que se ejecute la siguiente tubería:

* echo "Alias /adminer.php /usr/share/adminer/adminer.php" | sudo tee /etc/apache2/conf-available/adminer.conf

5. hacemos un reload de la confgiracion de apache:

* sudo a2enconf adminer.conf
* sudo systemctl reload apache2

6. La ruta para entrar a adminer será la siguiente: https://localhost/adminer.php



# 3.Instalación de GoAcces.

## 3.1 Instalación:

1. Instalamos la última versión de goAccess:

* wget http://tar.goaccess.io/goaccess-1.2.tar.gz

2. Extraemos los ficheros:

* sudo tar -xzvf goaccess-1.2.tar.gz

3. Cambiamos al directorio de goaccess-1.2 y compilaremos GoAccess ejecutando el siguiente comando: 

* cd goaccess-1.2
* sudo ./configure --enable-utf8 --enable-geoip=legacy

4. Ejecutamos: "sudo make"

5. Instalamos GoAccess: "sudo make install"

En caso de que está opción nos diese algún fallo, podemos intentarlo de la siguiente manera:

1. Instalaremos GoAccess a través de un repositorio, para ello encesitamos descargarlo usando apt:

* echo "deb http://deb.goaccess.io/ $(lsb_release -cs) main" | sudo tee -a /etc/apt/sources.list.d/goaccess.list
* wget -O - https://deb.goaccess.io/gnugpg.key | sudo apt-key add –

2. Actualizamos el repositorio: "sudo apt update -y"

3. Instalamos GoAccess: "sudo apt install goaccess -y"

## 3.2 Ejecución:

1. Analizamos el registro del servidor web:

* sudo goaccess /var/log/apache2/access.log --log-format=COMBINED

2. Una vez encontramos las estadisticas del servidor web Apache en tiempo real, podemos generar un reporte en formato html ejecutando la siguiente línea:

* sudo goaccess /var/log/apache2/access.log --log-format=COMBINED -a -o /var/www/html/report.html

3. Accedemos a dicho reporte: 

* hhtps://hostname/report.html



# 4. .htcaccess.

1. Crear y ubicar un fichero .htcaccess:

debes de abrir un bloc de notas e introducir el código necesario, debes guardarlo en (.txt) y los subes por FTP a la carpeta donde quieres que se aplique. Una vez esté dentro del servidor, modifica el nombre del fichero por el de ".htcaccess" y haz lo mismo con el fichero ".htpasswd".

2. Configuración:

en el ".htpasswd" introducimos lo siguiente:

user:AAAAAA

* user: usuario
* AAAAAA: contraseña

















