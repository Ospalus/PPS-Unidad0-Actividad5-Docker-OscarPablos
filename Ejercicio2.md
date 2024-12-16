# Ejercicio 2 #

### Enunciado ##

### Ejercicio para entregar

# Servidor web #

- Arranca un contenedor que ejecute una instancia de la imagen php:7.4-apache, que se llame web y que sea accesible desde tu equipo en el puerto 8000.
- Colocar en el directorio raíz del servicio web (/var/www/html) de dicho contenedor un fichero llamado index.html con el siguiente contenido:

<h1>HOLA SOY XXXXXXXXXXXXXXX</h1>

Deberás sustituir XXXXXXXXXXX por tu nombre y tus apellidos.


- Colocar en ese mismo directorio raíz un archivo llamado index.php con el siguiente contenido:

> <?php echo phpinfo(); ?>

- Para crear los ficheros tienes tres alternativas:
    - Ejecutando bash de forma interactiva en el contenedor y creando los ficheros.
    - Ejecutando un comando echo en el contenedor con docker exec.
    - Usando docker cp como hemos visto en el ejercicio 5.

# Servidor de base de datos
- Arrancar un contenedor que se llame bbdd y que ejecute una instancia de la imagen mariadb para que sea accesible desde el puerto 3336.
- Antes de arrancarlo visitar la página del contenedor en Docker Hub y establecer las variables de entorno necesarias para que:

    - La contraseña de root sea root.
    - Crear una base de datos automáticamente al arrancar que se llame prueba.
    - Crear el usuario invitado con las contraseña invitado.

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo que desde el navegador muestre el fichero index.html.
- Pantallazo que desde el navegador muestre el fichero index.php.
- Pantallazo donde se vea el tamaño del contenedor web después de crear los dos ficheros.
- Pantallazo donde desde un cliente de base de datos (instalado en tu ordenador) se pueda observar que hemos podido conectarnos al servidor de base de datos con el usuario creado y que se ha creado la base de datos prueba (show databases). El acceso se debe realizar desde el ordenador que tenéis instalado docker, no hay que acceder desde dentro del contenedor, es decir, no usar docker exec.
- Pantallazo donde se comprueba que no se puede borrar la imagen mariadb mientras el contenedor bbdd está creado.

## Desarrollo ##

# Servidor web

Lo primero que tenemos que hacer es arrancar el contenedor, para ello vamos a ejecutar el siguiente comando para iniciar un contenedor basado en la imagen php:7.4-apache:

>docker run -dit --name web -p 8000:80 php:7.4-apache

**Explación de comandos**:

- **-dit**: Inicia el contenedor en modo interactivo y en segundo plano.
- **--name web**: Nombra el contenedor como web.
- **-p 8000:80**: Mapea el puerto 8000 de tu máquina al puerto 80 del contenedor.
- **php:7.4-apache**: Especifica la imagen a utilizar.

 Si todo ha ido bien, deberíamos tener algo así:

 ![8](/Imágenes_png/8.png) 

Ahora tenemos que crear los archivos *index.html* e *index.php* en el contenedor, para ello, invocamos el comando:

>               docker exec -it web bash


![9](/Imágenes_png/9.png) 

Ahora navegamos al directorio raíz del servidor web, editamos el index.html para poner nuestro nombre y nuestros apellidos.

![10](/Imágenes_png/10.png) 

Después creamos el archivo *index.php*. Para ello invocamos el comando:

>       echo "<?php phpinfo(); ?>" > index.php

![11](/Imágenes_png/11.png) 

Después salimos del contenedor invocando **exit**. Ahora vamos al navegador y accedemos a la dirección para comprobar el contenido de index.html:

>http://localhost:8000/index.html 

![12](/Imágenes_png/12.png) 

y a la dirección para ver el archivo index.php 

>http://localhost:8000/index.php 

![13](/Imágenes_png/13.png) 

# Servidor de base de datos

Arranca el contenedor bbdd ejecutando el siguiente comando:

>docker run -dit --name bbdd -p 3336:3306 \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=prueba \
  -e MYSQL_USER=invitado \
  -e MYSQL_PASSWORD=invitado \
  mariadb

Explicación de parámetros:

- -e MYSQL_ROOT_PASSWORD=root: Configura la contraseña de root.
- -e MYSQL_DATABASE=prueba: Crea automáticamente una base de datos llamada prueba.
- -e MYSQL_USER=invitado y -e MYSQL_PASSWORD=invitado: Crea un usuario invitado con la contraseña invitado.

![14](/Imágenes_png/14.png) 

