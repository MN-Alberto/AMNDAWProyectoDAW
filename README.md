
# CFGS Desarrollo de Aplicaciones Web


- [CFGS Desarrollo de Aplicaciones Web](#cfgs-desarrollo-de-aplicaciones-web)
  - [1. Entorno de Desarrollo](#1-entorno-de-desarrollo)
    - [1.1 Ubuntu Server 24.04.3 LTS](#11-ubuntu-server-24043-lts)
      - [1.1.1 **Configuración inicial**](#111-configuración-inicial)
        - [Nombre y configuraicón de red](#nombre-y-configuraicón-de-red)
      - [Comandos de comprobación:](#comandos-de-comprobación)
        - [**Actualizar el sistema**](#actualizar-el-sistema)
        - [**Configuración fecha y hora**](#configuración-fecha-y-hora)
        - [**Cuentas administradoras**](#cuentas-administradoras)
        - [**Cuentas no administradoras**](#cuentas-no-administradoras)
        - [**Comprobar cuentas:**](#comprobar-cuentas)
        - [**Habilitar cortafuegos**](#habilitar-cortafuegos)
      - [1.1.2 Instalación del servidor web](#112-instalación-del-servidor-web)
        - [Instalación](#instalación)
        - [Verficación del servicio](#verficación-del-servicio)
        - [Comprobación del servidor](#comprobación-del-servidor)
        - [Virtual Hosts](#virtual-hosts)
        - [Permisos y usuarios](#permisos-y-usuarios)
      - [1.1.3 PHP8.3-fpm](#113-php83-fpm)
        - [Instalación](#instalación-1)
        - [Verificación del servicio](#verificación-del-servicio)
        - [Comprobación del servidor](#comprobación-del-servidor-1)
      - [1.1.4 MySQL](#114-mysql)
      - [1.1.5 XDebug](#115-xdebug)
      - [1.1.6 DNS](#116-dns)
      - [1.1.7 SFTP](#117-sftp)
      - [1.1.8 Apache Tomcat](#118-apache-tomcat)
      - [1.1.9 LDAP](#119-ldap)
    - [1.2 Windows 11](#12-windows-11)
      - [1.2.1 **Configuración inicial**](#121-configuración-inicial)
        - [**Nombre y configuración de red**](#nombre-y-configuración-de-red)
        - [**Cuentas administradoras**](#cuentas-administradoras-1)
      - [1.2.2 **Navegadores**](#122-navegadores)
      - [1.2.3 **MobaXterm**](#123-mobaxterm)
      - [1.2.4 **Netbeans**](#124-netbeans)
        - [Creación de proyectos](#creación-de-proyectos)
        - [Configuración de Git en NetBeans](#configuración-de-git-en-netbeans)
      - [1.2.5 **Visual Studio Code**](#125-visual-studio-code)
  - [2. GitHub](#2-github)
  - [3.Entorno de Explotación](#3entorno-de-explotación)

|  DAW/DWES Tema2 |
|:-----------:|
|![Alt](images/portada.jpg)|
| INSTALACIÓN, CONFIGURACIÓN Y DOCUMENTACIÓN DE ENTORNO DE DESARROLLO Y DEL ENTORNO DE EXPLOTACIÓN |

## 1. Entorno de Desarrollo

### 1.1 Ubuntu Server 24.04.3 LTS

Este documento es una guía detallada del proceso de instalación y configuración de un servidor de aplicaciones en Ubuntu Server utilizando Apache, con soporte PHP y MySQL

#### 1.1.1 **Configuración inicial**

##### Nombre y configuraicón de red

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
````
sudo netplan apply
````

##### **Actualizar el sistema**

```bash
sudo apt update
sudo apt upgrade
```

##### **Configuración fecha y hora**

[Establecer fecha, hora y zona horaria](https://somebooks.es/establecer-la-fecha-hora-y-zona-horaria-en-la-terminal-de-ubuntu-20-04-lts/ "Cambiar fecha y hora")
```
sudo timedatectl set-timezone Europe/Madrid
```

##### **Cuentas administradoras**

> - [X] root(inicio)
> - [X] miadmin/paso
> - [X] miadmin2/paso

##### **Cuentas no administradoras**
> - [X] operadorweb/paso

##### **Comprobar cuentas:**
```
cat /etc/passwd | grep nombreCuenta

id nombreCuenta

groups nombreCuenta

sudo useradd -m -G [grupos,grupos] -s /bin/bash miadmin3
```

##### **Habilitar cortafuegos**

Como activar cortafuegos
```
sudo ufw enable
```
Abrir el puerto del ssh(22)
```
sudo ufw allow 22
```
Comprobamos el estado del cortafuegos y puertos
```
sudo ufw status
```

Para borrar el puerto v6
```
sudo ufw status numbered

sudo ufw delete [numeroRegla]
```

#### 1.1.2 Instalación del servidor web

##### Instalación
```
  sudo apt install apache2
```
##### Verficación del servicio
```
  sudo service apache2 start
  sudo systemctl status apache2
  sudo ufw allow 80
```

##### Comprobación del servidor

  ![alt text](/images/8.png)

##### Virtual Hosts
##### Permisos y usuarios
  ```
  sudo adduser --home /var/www/html --ingroup www-data --shell /bin/bash operadorweb

  sudo chown -R operadorweb:www-data /var/www/html

  sudo chmod -R 775 /var/www/html
```
#### 1.1.3 PHP8.3-fpm
##### Instalación

 ```
  sudo apt install software-properties-common -y

  sudo add-apt-repository ppa:ondrej/php -y

  ls /etc/apt/sources.list.d/ | grep ondrej

  sudo apt update

  sudo apt install libapache2-mod-php8.3 php8.3-fpm -y

  sudo a2dismod mpm_prefork php8.3

  sudo a2enmod mpm_event proxy_fcgi
  ```

  Configuramos el sitio activo:

  ```
  
  cd /etc/apache2/sites-enabled/

  sudo nano 000-default.conf

  ProxyPassMatch ^/(.*\.php)$ unix:/run/php/php8.3-fpm.sock|fcgi://127.0.0.1/var/www/html
  ```

##### Verificación del servicio
   ```
    sudo service php8.3-fpm status
   ```

##### Comprobación del servidor

![alt text](/images/10.png)

![alt text](/images/9.png)

#### 1.1.4 MySQL
#### 1.1.5 XDebug
#### 1.1.6 DNS
#### 1.1.7 SFTP
#### 1.1.8 Apache Tomcat
#### 1.1.9 LDAP

### 1.2 Windows 11
#### 1.2.1 **Configuración inicial**
##### **Nombre y configuración de red**
##### **Cuentas administradoras**
#### 1.2.2 **Navegadores**
#### 1.2.3 **MobaXterm**
#### 1.2.4 **Netbeans**

##### Creación de proyectos

Para crear un proyecto en NetBeans deberemos de clicar en "File/New Project".

![alt text](/images/1.png)

Después clicaremos en la categoría de "PHP" y el tipo "PHP Application from Remote Server".
![alt text](/images/2.png)

Le daremos un nombre a nuestro proyecto y indicaremos la URL en la que se almacenará el proyecto.
![alt text](/images/3.png)

Indicaremos también la URL con la que buscaremos la página en el navegador (IP dek servidor) y el directorio de publicación.
![alt text](/images/4.png)

Mediante SFTP crearemos un archivo "index.html" dentro del directorio de publicación.
![alt text](/images/5.png)

Confirmaremos los archivos que queramos sincronizar.
![alt text](/images/6.png)

Y comprobaremos que cuando cambiamos algo en NetBeans se ejecutan los cambios en la web del servidor.
![alt text](/images/7.png)

##### Configuración de Git en NetBeans

En primer lugar deberemos de dirigirnos a nuestro repositorio de GitHub y copiaremos la URL del repositorio clicando en "<> Code" y en el apartado HTTPS.
![alt text](/images/11.png)

En NetBeans en el apartado "Team" deberemos de clicar en la opcion de "Git" y en la opción "Clonar..."
![alt text](/images/12.png)

Pegaremos la URL de nuestro repositorio y indicaremos el usuario y la contraseña de la cuenta de GitHub. Tmbién deberemos de indicar la carpeta de destino.
![alt text](/images/13.png)

Podremos a su vez indicar que ramas queremos de las que tiene el repositorio. (Si tubiera más aparecerían aquí).
![alt text](/images/14.png)

Indicaremos el directorio padre y el nombre de la clonacion.
![alt text](/images/15.png)

Al finalizar nos dirá si queremos crear un proyecto a partir del repositorio.

![alt text](/images/16.png)

Indicaremos el tipo de proyecto.
![alt text](/images/17.png)

Le pondremos un nombre y le indicaremos un directorio.
![alt text](/images/18.png)

Indicaremos la URL del servidor y su directorio de publicación.
![alt text](/images/19.png)

Confirmaremos los archivos.
![alt text](/images/20.png)

Y como podemos ver en el Repository Browser tenemos toda la información sobre la clonación.
![alt text](/images/21.png)

Al hacer clic derecho en "Source Files" de nuestro proyecto, en el apartado de "Git" podremos administrar todo, por ejemplo hacer un commit, megre etc.
![alt text](/images/22.png)

#### 1.2.5 **Visual Studio Code**

## 2. GitHub
## 3.Entorno de Explotación

---

> **Nombre y Apellidos**  
> Alberto Méndez Núñez
> Curso: 2025/2026  
> 2º Curso CFGS Desarrollo de Aplicaciones Web  
> Despliegue de aplicaciones web
