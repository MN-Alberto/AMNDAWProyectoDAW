### **1.2 Windows 11**
#### **1.2.1 **Configuración inicial**
##### **Nombre y configuración de red**
##### **Cuentas administradoras**
#### 1.2.2 **Navegadores**
#### 1.2.3 **MobaXterm**
#### 1.2.4 **Netbeans**

##### **Creación de proyectos**

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

##### **Configuración de Git en NetBeans**

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

#### 1.2.5 **phpDocumentor**

### Requisitos mínimos

Para poder utilizar phpDocumentor en el entorno de desarrollo es necesario cumplir los siguientes requisitos:

### Sistema

    Sistema Operativo: Ubuntu Server 20.04 LTS o superior

    Acceso: Usuario con permisos de instalación (sudo)

### Software:

PHP: versión 8.1 o superior

    Composer: versión 2.x

Extensiones PHP requeridas:

    php-cli
    php-xml
    php-mbstring
    php-curl

### Instalación de dependencias

Actualizar el sistema e instalar PHP con las extensiones necesarias:

```bash
sudo apt update
sudo apt install -y php php-cli php-xml php-mbstring php-curl unzip git
```

### Configuración de variables de entorno (nivel de cuenta)

Para que el comando phpDocumentor esté disponible desde cualquier ubicación, es necesario añadir Composer al PATH del usuario.

Editar el archivo .bashrc del usuario:
```bash
nano ~/.bashrc
```

Añadir la siguiente línea al final del archivo:
```bash
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
```

Aplicar los cambios:
```bash
source ~/.bashrc
```

### Uso de phpDocumentor
Desde la raíz del proyecto PHP:
```bash
phpDocumentor -d src -t docs
```

Donde:

    src -> contiene el código fuente PHP

    docs -> será el directorio donde se generará la documentación HTML

### Observaciones

    La instalación se realiza a nivel de cuenta, no del sistema completo.

    Cada usuario del servidor deberá configurar su propio PATH.

    Se recomienda mantener PHP y Composer actualizados para evitar incompatibilidades.



### Apache Tomcat

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
