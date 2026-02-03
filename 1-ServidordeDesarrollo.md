
## 📑 Índice

- [CFGS Desarrollo de Aplicaciones Web](#cfgs-desarrollo-de-aplicaciones-web)
  - [1. Entorno de Desarrollo](#1-entorno-de-desarrollo)
  - [1.1 Ubuntu Server 24.04.3 LTS](#11-ubuntu-server-240043-lts)
    - [1.1.1 Configuración inicial](#111-configuración-inicial)
      - [Nombre y configuración de red](#nombre-y-configuración-de-red)
    - [Comandos de comprobación](#comandos-de-comprobación)
      - [Configuración fecha y hora](#configuración-fecha-y-hora)
      - [Cuentas administradoras](#cuentas-administradoras)
      - [Cuentas no administradoras](#cuentas-no-administradoras)
      - [Comprobar cuentas](#comprobar-cuentas)
      - [Habilitar cortafuegos](#habilitar-cortafuegos)
    - [1.1.2 Instalación del servidor web](#112-instalación-del-servidor-web)
      - [Instalación](#instalación)
      - [Verificación del servicio](#verificación-del-servicio)
      - [Ficheros log](#ficheros-log)
      - [Comprobación del servidor](#comprobación-del-servidor)
    - [HTTP a HTTPS Server](#http-a-https-server)
    - [Redirección de HTTP a HTTPS Server](#redirección-de-http-a-https-server)
      - [Virtual Hosts](#virtual-hosts)
        - [Varios sitios HTTPS](#varios-sitios-https)
      - [Permisos y usuarios](#permisos-y-usuarios)
    - [1.1.3 PHP8.3-fpm](#113-php83-fpm)
      - [Instalación](#instalación-1)
      - [Verificación del servicio](#verificación-del-servicio-1)
      - [Comprobación del servidor](#comprobación-del-servidor-1)
    - [1.1.4 MariaDB](#114-mariadb)
      - [Instalación](#instalación-2)
      - [Módulos relacionados con PHP](#módulos-relacionados-con-php)
      - [Comprobación desde NetBeans](#comprobación-desde-netbeans)
    - [1.1.5 XDebug](#115-xdebug)
    - [1.1.6 DNS](#116-dns)
    - [1.1.7 SFTP](#117-sftp)
      - [Enjaular un usuario](#enjaular-un-usuario)
    - [1.1.8 Apache Tomcat](#118-apache-tomcat)
    - [1.1.9 LDAP](#119-ldap)
  - [2.0.0 PHPMyAdmin](#200-phpmyadmin)
  - [2.0.1 PHPDocumentor](#201-phpdocumentor)
  - [2.0.2 Apache Tomcat](#202-apache-tomcat)
    - [2.0.3 Instalación de Java Standard Edition Development Kit (JDK)](#instalación-de-java-standard-edition-development-kit-jdk)
    - [2.0.4 Instalación de Tomcat](#instalación-de-tomcat)

|  DAW/DWES Tema2 |
|:-----------:|
|![Alt](images/portada.jpg)|
| INSTALACIÓN, CONFIGURACIÓN Y DOCUMENTACIÓN DE ENTORNO DE DESARROLLO Y DEL ENTORNO DE EXPLOTACIÓN |

## 1. Entorno de Desarrollo

### 1.1 Ubuntu Server 24.04.3 LTS

Este documento es una guía detallada del proceso de instalación y configuración de un servidor de aplicaciones en Ubuntu Server utilizando Apache, con soporte PHP y MySQL

#### 1.1.1 **Configuración inicial**

##### Nombre y configuración de red

> **Nombre de la máquina**: daw-used\
> **Memoria RAM**: 2G\
> **Particiones**: 150G(/) | 350G (/var)\
> **Configuración de red interface**: enp0s3 \
> **Dirección IP** 10.199.9.104/22\
> **GW**: 10.199.8.1/22\
> **DNS**:  10.151.123.21
>           10.151.126.21


#### Comandos de comprobación:
> **Nombre de la máquina**: hostnamectl\
> **Memoria RAM**: free -h\
> **Particiones**: df -h\
> **Configuración de red interface**: ip a\
> **Dirección IP** ip a\
> **GW**: ip r\
> **DNS**:  resolvectl

Editar el fichero de configuración del interface de red  **/etc/netplan**,

```bash

# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s3:
      addresses:
       - 10.199.9.104/22
      nameservers:
         addresses:
         - 10.151.123.21
         - 10.151.126.21
         search: [educa.jcyl.es]
      routes:
        - to: default
          via: 10.199.8.1
  version: 2
````
Aplicamos la configuración de red con:
````bash
sudo netplan apply  #Aplica la configuración de red.
````

##### **Actualizar el sistema**

```bash
sudo apt update     #Recopila las posibles actualizaciones del sistema.
sudo apt upgrade    #Instala las actualizaciones recopiladas.
```

---

##### **Configuración fecha y hora**

[Establecer fecha, hora y zona horaria](https://somebooks.es/establecer-la-fecha-hora-y-zona-horaria-en-la-terminal-de-ubuntu-20-04-lts/ "Cambiar fecha y hora")
```bash
sudo timedatectl set-timezone Europe/Madrid   #Establece la fecha y hora a la zona horaria "Europe/Madrid".
```

---

##### **Cuentas administradoras**

> - [X] root(inicio)
> - [X] miadmin/paso
> - [X] miadmin2/paso
> - [X] adminsql/paso

##### **Cuentas no administradoras**
> - [X] operadorweb/paso

##### **Comprobar cuentas:**
```bash
cat /etc/passwd | grep nombreCuenta   #Muestra  las líneas del fichero "/etc/passwd" en las que aparezca el nombreCuenta que indicamos. 

id nombreCuenta   #Muestra los grupos del usuario.

groups nombreCuenta   #Muestra los grupos del usuario.

sudo useradd -m -G [grupos,grupos] -s /bin/bash miadmin3    #Añade un nuevo usuario a los grupos indicados y le indica un shell.
```

---

##### **Habilitar cortafuegos**

Como activar cortafuegos
```bash
sudo ufw enable   #Habilita el cortafuegos.
```
Abrir el puerto del ssh(22)

```bash
sudo ufw allow 22   #Permite la conexión por el puerto 22.
```
Comprobamos el estado del cortafuegos y puertos
```bash
sudo ufw status   #Muestra el estado del cortafuegos y los puertos abiertos.
```

Para borrar el puerto v6
```bash
sudo ufw status numbered  #Muestra el estado del cortafuegos mostrando el número de regla que identifica a cada puerto.  

sudo ufw delete [numeroRegla]   #Elimina el puerto al indicarle su número de regla correspondiente.
```

#### **1.1.2 Instalación del servidor web**

##### **Instalación**
```bash
  sudo apt install apache2    #Instalamos el servicio apache.
```
##### **Verficación del servicio**
```bash
  sudo service apache2 start    #Arrancamos el servicio apache.
  sudo systemctl status apache2   #Mostramos el estado del servicio.
  sudo ufw allow 80   #Habilitamos el puerto 80 en el cortafuegos ya que es el que utiliza por defecto para escuchar las peticiones del navegador del cliente.
```
##### **Ficheros log**
Los ficheros de log de apache se almacenan en "/var/log/apache2".

##### **Comprobación del servidor**

  ![alt text](images/8.PNG)

---

#### **HTTP a HTTPS Server**

Así funciona HTTPS:
  ![alt text](images/imagenhttps.png)

En primer lugar habilitamos el modulo "ssl"

```bash
sudo a2enmod ssl    #Habilitamos el módulo ssl.
```

Después crearemos el certificado autofirmado:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/amn-used.key -out /etc/ssl/certs/amn-used.crt

#Creamos un certificado autofirmado y almacenamos la clave privada en "/etc/ssl/private" y el certificado en "/etc/ssl/certs".
```

Comprobamos que se ha creado correctamente con:

```bash
sudo ls /etc/ssl/certs | grep amn-used    #Comprobamos que el certificado se ha creado correctamente.

sudo ls /etc/ssl/private | grep amn-used    #Comprobamos que la clave privada se ha creado correctamente.
```
Reiniciamos el servicio de apache:

```bash
sudo systemctl restart apache2
```

Nos dirigiremos al directorio "/etc/apache2/sites-available" y haremos una copia del fichero "default-ssl.conf"

```bash
sudo cp default-ssl.conf amn-used.conf
```

Dentro de la copia cambiaremos el nombre del certificado y de la clave por los que indicamos al crearlo:

![alt text](images/htps.PNG)

Después activaremos el nuevo sitio:

```bash
sudo a2ensite amn-used.conf
```

Reiniciamos el servicio de apache:

```bash
sudo systemctl restart apache2
```

Y por último habilitaremos el puerto 443 en el cortafuegos:

```bash
sudo ufw allow 443
```

Comprobamos:

![alt text](images/certPrueba.PNG)

#### **Redirección de HTTP a HTTPS Server**
Para redireccionar apache HTTP a HTTPS deberemos de habilitar el módulo "rewrite" y editar el fichero ".htaccess" del directorio raíz de publicación y añadiremos las siguientes directivas.

En primer lugar habilitaremos el módulo "rewrite":

```
sudo a2enmod rewrite
```

Después reiniciaremos apache:

```
sudo systemctl restart apache2
```

A continuación en el fichero ".htaccess" del raíz de publicación podremos las siguientes directivas:

![alt text](images/htaccessRedireccion.PNG)

Y al finalizar reiniciaremos de nuevo apache y podremos comprobar que al acceder a la URL mediante http el servidor redirecciona automáticamente a https.

##### **Virtual Hosts**
Vamos a configurar un sitio virtual llamado "sitio1.albertomennun.ieslossauces.es".

Para ello en primer lugar, deberemos de acceder al panel de configuración de nuestro hosting, y clicaremos en el apartado "Hosting y DNS" y en la opción "DNS"
![alt text](images/SITIOS/0.1.PNG)

A continuación clicaremos en "+ Añadir registro"
![alt text](images/SITIOS/0.2.PNG)

Después le podremos indicar el tipo de registro, el nombre de dominio, el TTL (Time To Life) y la dirección IP de nuestro servidor.
![alt text](images/SITIOS/0.3.PNG)


Como podemos comprobar se ha creado correctamente.
![alt text](images/SITIOS/0.4.PNG)


Ahora vamos a configurar nuestro sitio en nuestro servidor apache.

En primer lugar deberemos de ir al directorio "/etc/apache2/sites-available" y copiaremos el sitio "000-default.conf" con el nombre de nuestro sitio remplazando los puntos por guiones .conf "sitio1-albertomennun-ieslossauces-es.conf".

![alt text](images/SITIOS/1.PNG)


Editaremos el fichero y añadiremos el "ServerName" y modificaremos el "DocumentRoot", el "ErrorLog" y el "ProxyPassMatch".
![alt text](images/SITIOS/4.PNG)


A continuación nos dirigiremos al directorio "/var/www/usuarioEnjaulado1" y crearemos el directorio "error".
![alt text](images/SITIOS/5.PNG)


Después comprobaremos los permisos de la carpeta error y modificaremos su propietario para que sea "usuarioEnjaulado1" y al grupo "www-data". También cambiaremos los permisos de la carpeta a 775.
![alt text](images/SITIOS/6.PNG)

Luego deberemos de habilitar el sitio y reiniciar el servicio apache.
![alt text](images/SITIOS/7.PNG)

A continuación nos conectaremos mediante SFTP con el usuario usuarioEnjaulado1 y en la carpeta htdocs pegaremos la aplicación que queremos subir.
![alt text](images/SITIOS/8.1.PNG)

Después modificaremos el archivo ".htaccess" y indicaremos el "DirectoryIndex" que en este caso es "indexProyectoTema4.php".

![alt text](images/SITIOS/8.PNG)

Y por ultimo comprobamos que accediendo en el navegador a "sitio1.albertomennun.ieslossauces.es" nos llevará a nuestro nuevo sitio.

![alt text](images/SITIOS/9.PNG)

###### **Varios sitios HTTPS**
A continuación vamos a hacer que podamos tener varios sitios HTTPS en nuestro servidor web.


En primer lugar crearemos un certificado autofirmado, y le daremos nombre a la clave privbada y al certificado:

![alt text](images/variosSitiosHTTPS/1.PNG)

En la información que tenemos que introducir al crear el certificado, en el apartado de "Common Name" deberemos de introducir el nombre que va a tener nuestro sitio, en este caso "sitio1.albertomennun.ieslossauces.es"

![alt text](images/variosSitiosHTTPS/2.PNG)

A continuación nos dirigiremos al directorio "/etc/apache2/sites-available" y haremos una copia del archivo "default-ssl.conf" y la llamaremos "sitio1-ssl.conf"

![alt text](images/variosSitiosHTTPS/3.PNG)

Lo editaremos, y deberemos de introduicir un "ServerName" y un "DocumentRoot".
También deberemos editar los "ErrorLog" poniendo un nombre de archivo diferente al por defecto para en caso de algun error en nuestra página poder identificar facilmente el archivo log.ç
Importante también cambiar el certificado y la clave como se ve en la parte inferior de la captura.

![alt text](images/variosSitiosHTTPS/4.PNG)

Guardaremos el archivo y activaremos el sitio que acabamos de configurar y reiniciaremos el servicio apache.

![alt text](images/variosSitiosHTTPS/5.PNG)

Al hacer esto ya funcionaria nuestro sitio HTTPS, como ejemplo he subido una release de el proyecto tema 4 de DWES de Gonzalo y como se ve en la captura funciona correctamente.

![alt text](images/variosSitiosHTTPS/6.PNG)

Funciona como esperabamos pero vamos a redireccionar HTTP a HTTPS para que siempre que accedamos accedamos con HTTPS.
Para ello en el archivo ".htacces" del proyectoTema4 de gonzalo que hemos subido a nuestro sitio, deberemos de indicar el "DirectoryIndex" (indice de nuestra página) y añadiremos las líneas que corresponden al módulo "Rewrite" para hacer la redirección de HTTP a HTTPS.
Importante en la línea "RewriteRule" indicar la URL con HTTPS ya que es a la URL a la que se va a redireccionar.

![alt text](images/variosSitiosHTTPS/7.PNG)

##### **Permisos y usuarios**
Creamos una cuenta para la publicación de contenidos en nuestra web:
  ```
  sudo adduser --home /var/www/html --ingroup www-data --shell /bin/bash operadorweb

  sudo chown -R operadorweb:www-data /var/www/html

  sudo chmod -R 775 /var/www/html
  
```

#### **1.1.3 PHP8.3-fpm**
##### **Instalación**

 ```

  sudo apt install php8.3-fpm php8.3 -y

  sudo a2enmod mpm_event proxy_fcgi
  ```

  Configuramos el sitio activo:

  ```
  
  cd /etc/apache2/sites-enabled/

  sudo nano 000-default.conf

  ProxyPassMatch ^/(.*\.php)$ unix:/run/php/php8.3-fpm.sock|fcgi://127.0.0.1/var/www/html
  ```

##### **Verificación del servicio**
   ```
    sudo service php8.3-fpm status
   ```

##### **Comprobación del servidor**

![alt text](images/10.PNG)

![alt text](images/9.PNG)

#### **1.1.4 MariaDB**
#### **Instalación**
En primero lugar actualizaremos nuestro servidor con:
```
    sudo apt update
```
Luego instalaremos el servicio "mariadb-server":
```
    sudo apt install mariadb-server
```
Al instalarlo iniciaremos el servicio:
```
    sudo service mariadb start
```
Y comprobaremos el estado con:
```
    sudo service mariadb status
```
Comprobaremos la version de mariadb con:
```
    sudo mariadb --version
```
Entraremos en el fichero de configuración de mariaDB y cambiaremos el apartado "bind-address" por "0.0.0.0":
    sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
![alt text](images/confMariadb.png)

Comprobamos el puerto por defecto que utiliza mariaDB (3306):
![alt text](images/puertoMariadb.png)

A continuación deberemos de crear un usuario "adminsql" de contraseña "paso".
Para ello entraremos en la consola de MariaDB con "sudo mariadb" y los siguientes comandos:

Creación del usuario:

![alt text](images/usuarioSql.png)

Configuración de permisos de administrador:

![alt text](images/permisosUsuario.png)

Mysql tiene un modo de instalación seguro para evitar brechas de seguridad, lo ejecutaremos con "sudo mysql_secure_installation" y responderemos a las preguntas en función de nuestras preferencias:
![alt text](images/mysqlSi.png)

![alt text](images/mysqlSi2.png)

Una de las preguntas ha sido si queríamos que el usuario "root" tuviera contraseña, lo comprobamos con el siguiente comando:
![alt text](images/compRoot.png)


#### **Módulos relacionados con PHP**
Deberemos de instalar el módulo que integra mysql con php8.3-fpm con:
![alt text](images/moduloMysql.png)

Comprobaremos que se ha instalado correctamente con:
![alt text](images/comprobarModulos.png)

#### **Comprobación desde NetBeans**
En primer lugar deberemos de ir al apartado de "Services" y hacer clic derecho en "Databases". Deberemos de entrar en "New Connection...":

![alt text](images/comprobarSql/1.png)

A continuación deberemos de elegir el driver que queremos utilizar, en este caso MariaDB (MySQL-compatible) y indicarle el archivo del driver que hemos bajado de internet:

![alt text](images/comprobarSql/2.png)

Deberemos de indicar la IP de nuestro servidor, el puerto, la base de datos a la que queremos conectarnos, y el usuario y password que hemos creado anteriormente:
![alt text](images/comprobarSql/3.png)


Como podemos comprobar nos hemos conectado correctamente:
![alt text](images/comprobarSql/4.png)

Para ejecutar un script deberemos de hacer click derecho en la conexión y entraremos en "Execute Command":
![alt text](images/comprobarSql/5.png)


#### **1.1.5 XDebug**

Vamos a instalar XDebug para poder utilizarlo en nuestro IDE.

Para ello, en primer lugar deberemos de instalarlo con el comando:
```bash
  sudo apt install php8.3-xdebug
```
![alt text](images/xDebug/1.PNG)

A continuación hacemos "ls" dentro de "/etc/php/8.3/apache2/conf.d" para comporbar que xdebug se ha instalado correctamente.
![alt text](images/xDebug/2.PNG)

En el archivo de configuración de xdebug, deberemos de poner las siguientes lineas:

![alt text](images/xDebug/5.PNG)

Y a continuación deberemos de seguir en el Cliente de Desarrollo.


#### **1.1.6 DNS**
#### **1.1.7 SFTP**


##### **Enjaular un usuario**

Vamos a enjaular el usuario "usuarioEnjaulado1" en el directorio "/var/www/usuarioEnjaulado1".

Para ello, en primer lugar, deberemos de crear un grupo en el que vamos a meter los usuarios que queramos enjaular:
```
  sudo addgroup sftpusers
```
![alt text](images/enjaular/1.png)

A continuación crearemos el usuario "usuarioEnjaulado1", haciendo que pertenezca a los grupos "www-data" y "sftpusers", además haremos que el home del usuario sea "/var/www/usuarioEnjaulado1":

![alt text](images/enjaular/2.PNG)

Después cambiaremos el propietario del directorio "/var/www/usuarioEnjaulado1" a "root" y cambiaremos los permisos a solo lectura:

![alt text](images/enjaular/3.PNG)

Crearemos la carpeta "htdocs" en "/var/www/usuarioEnjaulado1" y cambiaremos los permisos de la carpeta y su propietario que ahora será "usuarioEnjaulado1":

![alt text](images/enjaular/4.PNG)

A continuación nos dirigiremos al directorio "/etc/ssh" y haremos una copia de seguridad del fichero "sshd_config" y editaremos el fichero existente, no la copia:

![alt text](images/enjaular/5.PNG)

![alt text](images/enjaular/6.PNG)

Reiniciaremos el servicio:

```
  sudo service ssh restart
```

Por ultimo nos conectaremos mediante sftp y el usuario "usuarioEnjaulado1" y comprobaremos que el usuario no puede moverse de el directorio indicado:

![alt text](images/enjaular/7.PNG)


#### **1.1.8 Apache Tomcat**
#### **1.1.9 LDAP**
#### **2.0.0 PHPMyAdmin**
Vamos a instalar "phpmyadmin" en nuestro servidor web.
En primer lugar crearemos un archivo "listarmodulos.txt" en el que almacenaremos el resultado de el comando "php -m", que muestra todos los módulos instalados referentes a PHP. Hacemos esto para al finalizar la instalación de "phpmyadmin" comprobar los módulos adicionales de PHP que se han instalado.

![alt text](images/phpMyadmin/1.PNG)

Instalamos "phpmyadmin"

![alt text](images/phpMyadmin/2.PNG)

A continuación deberemos de elejir la opción "apache2" para que phpmyadmin se configure automaticamente para apache2, seleccionaremos con la barra espaciadora y continuaremos.

![alt text](images/phpMyadmin/3.PNG)

Elejiremos la opción "yes" para configurar la base de datos de "phpmyadmin".

![alt text](images/phpMyadmin/4.PNG)

Le pondremos una contraseña a MySQL.

![alt text](images/phpMyadmin/5.PNG)

Y por último antes de comprobar haremos un nuevo archivo en el que listaremos los módulos de php de nuevo para comprobar los nuevos que se han instalado.

![alt text](images/phpMyadmin/6.PNG)

#### **2.0.1 PHPDocumentor**

Antes de instalarlo, un requisito minimo indispensable es tener instalado PHP 8.1 o superior.

### Comprobamos la versión con:
```bash
php -v
```

### Después deberemos de instalar composer:
```bash
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

php composer-setup.php

sudo mv composer.phar /usr/local/bin/composer

composer --version
```

### Instalamos phpDocumentor globalmente
```bash
composer global require phpdocumentor/phpdocumentor
```

Añade Composer al PATH si no está ya:
```bash
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Comprueba la instalación:
```bash
phpDocumentor --version
```

#### **2.0.2 Apache Tomcat**

Vamos a instalar Apache Tomcat en nuestro equipo anfitrión. Para ello necesitamos unos requisitos mínimos:

Tomcat necesita Java para funcionar:

    Tomcat 10.x → Java 11 o superior

    Tomcat 9.x → Java 8 o superior

    Tomcat 8.5 → Java 7 o superior


Tomcat es multiplataforma:

    Windows

    Linux

    macOS

    Unix

(No requiere uno específico, solo que soporte Java)

Memoria RAM

    Mínimo: 512 MB

    Recomendado: 1 GB o más (especialmente si ejecutas apps web)

Espacio en disco

    Mínimo: ~100 MB

    Recomendado: más espacio según las aplicaciones que vayamos a desplegar

Puertos

    Puerto 8080 libre (por defecto)

    Puerto 8005 (shutdown)

    Puerto 8009 (AJP, opcional)

Requisitos recomendados (para producción)

    Java LTS (11 o 17)

    2 GB de RAM o más

    SSD

    Configuración de variables de entorno y permisos adecuados

###  INSTALACIÓN DE JAVA STANDARD EDITION DEVELOPMENT KIT (JDK) 

#### 1. Iniciar sesión en Windows

#### 2. Descargar Java SE Development Kit en https://adoptium.net/es/

#### 3. Elige la versión 64 bits de instalación, y descargue el fichero

#### 4. Instalar la versión JDK descargada.

#### 5. Comprobar la versión con el comando java -version y javac -version

```cmd
C:\Users\alberto.mennun>java -version
openjdk version "11.0.22" 2024-01-16 LTS
OpenJDK Runtime Environment Microsoft-8909545 (build 11.0.22+7-LTS)
OpenJDK 64-Bit Server VM Microsoft-8909545 (build 11.0.22+7-LTS, mixed mode, sharing)

C:\Users\alberto.mennun>javac -version
javac 11.0.22
```

#### 6. Comprobar las variables del sistema
Deberemos de tener las variables "CLASSPATH" y "JAVA_HOME", la variable JAVA_HOME deberá contener la url donde tenemos almacenado el JDK.

### INSTALACIÓN DE TOMCAT

#### 1. Descarga Apache Tomcat en https://tomcat.apache.org/

Descargaremos la versión que necesitemos en función de nuestro sistema operativo y las especificaciones de nuestro equipo.

¿Qué versión de Java utilizar?

    Java 11 o superior (ideal: Java 17 o 21)
    Es la versión estable y recomendada hoy
    Soporte a largo plazo
    Ideal para proyectos nuevos y aprendizaje

#### 2. Descargar el Core con extensión .zip

#### 3. En el disco de datos, en una carpeta llamada software la descomprimiremos

#### 4. A continuación, iremos a Apache Netbeans y añadiremos el Servidor Tomcat. En el menú Tools→ Server. En “Servers” hacemos clic en el botón derecho “Add Server Instance”

![alt text](apacheTomcat/1.png)

![alt text](apacheTomcat/2.png)

Elegiremos la opción de Apache Tomcat

![alt text](apacheTomcat/3.png)

El "Server Location" será la ubicación de la carpeta en la que se encuentra nuestro Apache Tomcat. De usuario y contraseña utilizaremos "tomcat", NO ES RECOMENDABLE UTILIZAR ESTE USUARIO Y CONTRASEÑA EN EXPLOTACIÓN.

![alt text](apacheTomcat/4.png)

A continuación arrancaremos el servidor, en los servicios de NetBeans, en el apartado "Servers", haremos clic derecho en el que acabamos de crear y clicaremos en "Start".

![alt text](apacheTomcat/5.png)

Como vemos, al arrancarlo, podemos ver todas las páginas que tiene nuestro servidor.

![alt text](apacheTomcat/6.png)

Si en un navegador accedemos a la url http://localhost:8080 podremos acceder al panel de control de Apache Tomcat y así comprobar y monitorizar su funcionamiento.

![alt text](apacheTomcat/7.png)

Tenemos 3 apartados disponibles, pero solo podemos acceder a 1 de ellos libremente sin cambiar ningún rol. A apartado "Server Status".

![alt text](apacheTomcat/8.png)

Como vemos, si intentamos acceder a "Manager App" y "Host Manager", nos dará un error de acceso denegado:

![alt text](apacheTomcat/13.png)

Si queremos acceder a los apartados de "Manager App" y "Host Manager", deberemos de dirigirnos al archivo "tomcat-users.xml", que se ubica en la carpeta "/conf" dentro de la carpeta que contiene todos los archivos de Apache Tomcat. Cuando lo hayamos ubicado, deberemos editarlo:

![alt text](apacheTomcat/9.png)

Al editar el archivo, justamente al final de este, tendremos el usuario que creamos al añadir nuestro servidor Tomcat en NetBeans, "tomcat" de contraseña también "tomcat". Este usuario, viene con los roles "manager-script" y "admin" por defecto, pero si queremos acceder a los apartados de "Manager App" y "Host Manager", deberemos de añadirle los roles de "manager-gui" y "admin-gui".

![alt text](apacheTomcat/10.png)

Tras hacerlo podremos acceder libremente a dichos apartados:

![alt text](apacheTomcat/11.png)

![alt text](apacheTomcat/12.png)