## 📑 Índice

- [📑 Índice](#-índice)
      - [**1. Creación de proyectos**](#1-creación-de-proyectos)
      - [**2. Configuración de Git en NetBeans**](#2-configuración-de-git-en-netbeans)
    - [3. **xDebug**](#3-xdebug)
    - [4. **phpDocumentor**](#4-phpdocumentor)
  - [5. Apache Tomcat](#5-apache-tomcat)
  - [6. Comprobación de servidor HTTP](#6-comprobación-de-servidor-http)
  - [7. Comprobación de servidor HTTPS](#7-comprobación-de-servidor-https)


##### **1. Creación de proyectos**

Para crear un proyecto en NetBeans deberemos de clicar en "File/New Project".

![alt text](images/1.png)

Después clicaremos en la categoría de "PHP" y el tipo "PHP Application from Remote Server".
![alt text](images/2.png)

Le daremos un nombre a nuestro proyecto y indicaremos la URL en la que se almacenará el proyecto.
![alt text](images/3.png)

Indicaremos también la URL con la que buscaremos la página en el navegador (IP dek servidor) y el directorio de publicación.
![alt text](images/4.png)

Mediante SFTP crearemos un archivo "index.html" dentro del directorio de publicación.
![alt text](images/5.png)

Confirmaremos los archivos que queramos sincronizar.
![alt text](images/6.png)

Y comprobaremos que cuando cambiamos algo en NetBeans se ejecutan los cambios en la web del servidor.
![alt text](images/7.png)

##### **2. Configuración de Git en NetBeans**

En primer lugar deberemos de dirigirnos a nuestro repositorio de GitHub y copiaremos la URL del repositorio clicando en "<> Code" y en el apartado HTTPS.
![alt text](images/11.png)

En NetBeans en el apartado "Team" deberemos de clicar en la opción de "Git" y en la opción "Clonar..."
![alt text](images/12.png)

Pegaremos la URL de nuestro repositorio y indicaremos el usuario y la contraseña de la cuenta de GitHub. También deberemos de indicar la carpeta de destino.
![alt text](images/13.png)

Podremos a su vez indicar que ramas queremos de las que tiene el repositorio. (Si tuviera más aparecerían aquí).
![alt text](images/14.png)

Indicaremos el directorio padre y el nombre de la clonación.
![alt text](images/15.png)

Al finalizar nos dirá si queremos crear un proyecto a partir del repositorio.

![alt text](images/16.png)

Indicaremos el tipo de proyecto.
![alt text](images/17.png)

Le pondremos un nombre y le indicaremos un directorio.
![alt text](images/18.png)

Indicaremos la URL del servidor y su directorio de publicación.
![alt text](images/19.png)

Confirmaremos los archivos.
![alt text](images/20.png)

Y como podemos ver en el Repository Browser tenemos toda la información sobre la clonación.
![alt text](images/21.png)

Al hacer clic derecho en "Source Files" de nuestro proyecto, en el apartado de "Git" podremos administrar todo, por ejemplo hacer un commit, merge etc.
![alt text](images/22.png)

#### 3. **xDebug**

En nuestro IDE, deberemos de dirigirnos a "Tools/Options/PHP/Debugging", y deberemos de comprobar que el puerto de debugg es el 9003.

![alt text](images/xDebug/3.PNG)

#### 4. **phpDocumentor**

## Requisitos previos

Antes de empezar, asegúrate de tener instalado:

- Windows 10 u 11
- PHP 7.4 o superior
- Apache NetBeans 12 o superior
- Composer
- Acceso a la línea de comandos (CMD o PowerShell)

Verificar versión de PHP:

```bash
    php -v
```

Instalar Composer:

Descarga Composer desde:
https://getcomposer.org/Composer-Setup.exe

Ejecuta el instalador y asegúrate de que detecta tu instalación de PHP.

Verifica la instalación:

```bash
    composer --version
```

Instalar PHPDocumentor:

```bash
    composer global require phpdocumentor/phpdocumentor
```

Normalmente se instalará en C:\Users\TU_USUARIO\AppData\Roaming\Composer\vendor\bin

Añadir PHPDocumentor al PATH:

Deberemos de dirigirnos a las variables de entorno del sistema y editar la variable PATH, la editaremos y añadiremos la ruta C:\Users\TU_USUARIO\AppData\Roaming\Composer\vendor\bin

Comprobamos que PHPDocumentor funciona:

```bash
    phpdoc --version
```

Configuración de NetBeans:

    Abrir NetBeans

    Ir a File -> Open Project

    Seleccionar proyecto PHP

Configurar PHPDocumentor:

    Tools -> Options -> PHP -> PHPDocumentor

En el apartado PHPDocumento script escribiremos

```bash
    phpdoc
```

También podemos utilizar la ruta completa: C:\Users\TU_USUARIO\AppData\Roaming\Composer\vendor\bin\phpdoc.bat

Tras hacer esto, en nuestro proyecto es importante que haya comentarios PHPDoc.

Para generar la documentación, podremos hacerlo desde NetBeans y desde la línea de comandos:

### NetBeans:

Clic derecho sobre el proyecto

Seleccionar:

```bash
    Generate Documentation → PHPDocumentor
```

Elegir la carpeta de destino (por ejemplo docs/)


### Línea de Comandos:

Desde la raíz del proyecto ejecutar:

    src es la carpeta del código fuente

    docs es la carpeta donde se generará la documentación

```bash
    phpdoc -d src -t docs
```

Abre la carpeta docs

Ejecuta el archivo index.html


### Errores comunes

Error: phpdoc no se reconoce como comando

    Verificar que la ruta esté correctamente añadida al PATH

    Usar la ruta completa al ejecutable phpdoc.bat

Error: NetBeans no genera la documentación

    Revisar la ruta configurada en Tools -> Options -> PHP -> PHPDocumentor


### 5. Apache Tomcat

Vamos a desplegar un proyecto Maven/Web Aplication en nuestro servidor Apache Tomcat mediante NetBeans.

IMPORTANTE: Tener el servidor Tomcat arrancado antes de proceder.

En primer lugar clicaremos en "New Project" y seleccionaremos las opciones de "Java with Maven" y el tipo de proyecto será "Web Aplication".
![alt text](apacheTomcat/proyectoTomcat/1.PNG)

Indicaremos el nombre del proyecto y donde se va a encontrar, en este caso se llamará "AMNDAWProyectoTomcat" y se encuentra en "D:\ProyectosNetBeans". También cambiaremos el apartado "Version" a la 1.0, ya que es nuestra primera versión.
![alt text](apacheTomcat/proyectoTomcat/2.PNG)

A continuación indicaremos nuestro servidor, que en este caso será el servidor Tomcat que tenemos arrancado y la versión de Jakarta.
![alt text](apacheTomcat/proyectoTomcat/3.PNG)

Como podemos comprobar, se ha creado el proyecto correctamente.

![alt text](apacheTomcat/proyectoTomcat/4.PNG)

A continuación, vamos a crear un nuevo archivo de tipo "JSP"

![alt text](apacheTomcat/proyectoTomcat/5.PNG)

Lo llamaremos index, la localización será "Web pages" y utilizaremos la syntaxis estandar.

![alt text](apacheTomcat/proyectoTomcat/6.PNG)

También vamos a crear un "Servlet" .

![alt text](apacheTomcat/proyectoTomcat/6.5.PNG)

Lo llamaremos "login".

![alt text](apacheTomcat/proyectoTomcat/7.PNG)

Aquí podemos ver el Servlet del login.

![alt text](apacheTomcat/proyectoTomcat/8.PNG)

A continuación en las propiedades del proyecto, en el apartado "Run", comporbaremos que la configuración es la correcta.

![alt text](apacheTomcat/proyectoTomcat/9.PNG)

Después de hacer esto, si buscamos la URL "localhost:8080/AMNDAWProyectoTomcat/" podemos ver que aparece el mensaje "Hello World!"

![alt text](apacheTomcat/proyectoTomcat/10.PNG)

También si buscamos la URL "localhost:8080/AMNDAWProyectoTomcat/login" nos aparecerá la página del Servlet.

![alt text](apacheTomcat/proyectoTomcat/12.PNG)

Por último, si nos dirigimos al apartado "Servers" de NetBeans, podemos ver que se ha añadido el nuevo proyecto que acabamos de desplegar.

![alt text](apacheTomcat/proyectoTomcat/11.PNG)


### 6. Comprobación de servidor HTTP

  ![alt text](images/8.PNG)

### 7. Comprobación de servidor HTTPS

  ![alt text](images/certPrueba.PNG)