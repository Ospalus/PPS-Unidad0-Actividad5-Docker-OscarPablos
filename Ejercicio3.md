# Ejercicio 3 #

### Enunciado ##

### Ejercicio para entregar

Entrega uno de estos dos ejercicios (si estás muy aburrido puedes entregar los dos):

### Creación y uso de volúmenes ###

1. Crear los siguientes volúmenes con la orden docker volume: volumen_datos y volumen_web.
2. Una vez creados estos contenedores:
    - Arrancar un contenedor llamado c1 sobre la imagen php:7.4-apache que monte el volumen_web en la ruta /var/www/html y que sea accesible en el puerto 8080.
    - Arrancar un contenedor llamado c2 sobre la imagen mariadb que monte el volumen_datos en la ruta /var/lib/mysql y cuya contraseña de root sea admin.

3. Intenta borrar el volumen volumen_datos, para ello tendrás que parar y borrar el contenedor c2 y tras ello borrar el volumen.
4. Copia o crea un fichero index.html al contenedor c1, accede al contenedor y comprueba que se está visualizando.
5. Borra el contenedor c1 y crea un contenedor c3 con las mismas características que c1 pero sirviendo en el puerto 8081.

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se puedan ver los dos volúmenes creados.
- Pantallazo con la orden correspondiente para arrancar el contenedor c1 usando el volumen_web.
- Pantallazo con la orden correspondiente para arrancar el contenedor c2 usando el volumen_datos.
- Pantallazo donde se vea el proceso para poder borrar el volumen_datos.
- Pantallazo donde se vea el borrado de c1 y la creación de c3.
- Pantallazo donde se vea el acceso al contenedor c3.

## Bind mount para compartir datos ##

1. Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido (Deberás sustituir ese XXXXXx por tu nombre.):

 <h1>HOLA SOY XXXXXX</h1>
2. Una vez hecho esto arrancar dos contenedores basados en la imagen php:7.4-apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor. Uno de ellos vamos a acceder con el puerto 8181 y el otro con el 8282. Y su nombres serán c1 y c2.
3. Modifica el contenido del fichero ~/saludo/index.html.
4. Comprueba que puedes seguir accediendo a los contenedores, sin necesidad de reiniciarlos.

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo con la orden correspondiente para arrancar el contenedor c1 (puerto 8181) realizando el bind mount solicitado.
- Pantallazo con la orden correspondiente para arrancar el contenedor c2 (puerto 8282) realizando el bind mount solicitado.
- Pantallazo donde se pueda apreciar que accediendo a c1 se puede ver el contenido de index.html.
- Pantallazo donde se pueda apreciar que accediendo a c2 se puede ver el contenido de index.html.
- Otro dos pantallazos (o uno) donde se vea accediendo a los contenedores después de modificar el fichero index.html.

## Resultados
### Creación y uso de volúmenes ###
1. Creamos los volúmenes volumen_datos y volumen_web con los siguientes comandos:

>docker volume create volumen_datos

>docker volume create volumen_web

Para confirmar que los volúmenes se han creado correctamente, usamos el siguiente comando para listarlos:

>docker volume ls

Esto mostrará los volúmenes creados:

![22](/Imágenes_png/22.png)

2. Arrancamos el contenedor c1 usando la imagen php:7.4-apache y montamos el volumen volumen_web en la ruta /var/www/html. Además, nos aseguramos de que sea accesible en el puerto 8080, para ello invocamos el comando:

>docker run -d --name c1 -p 8080:80 -v volumen_web:/var/www/html php:7.4-apache

![23](/Imágenes_png/23.png)

Arrancamos el contenedor c2 sobre la imagen mariadb, montando el volumen volumen_datos en /var/lib/mysql y configurando la contraseña de root como admin. 
Para ello invocamos el comando:

>docker run -d --name c2 -e MYSQL_ROOT_PASSWORD=admin -v volumen_datos:/var/lib/mysql mariadb

![24](/Imágenes_png/24.png)

3. Para borrar el volumen volumen_datos, primero debemos detener y eliminar el contenedor c2 que lo está usando. Luego, podremos borrar el volumen.
Para detener el contenedor invocamos el comando:

>docker stop c2

y para eliminarlo invocamos el comando:

>docker rm c2

Y después podremos borrar el volumen de datos, para ello invocamos el comando:

>docker volume rm volumen_datos

![25](/Imágenes_png/25.png)

4. Creamos un archivo index.html en el contenedor c1. Para ello
Copiamos o creamos un archivo index.html en el contenedor c1, para ello invocamos el comando:

>` echo "<html><body><h1>Hola, mundo!</h1></body></html>" > index.html `

>docker cp index.html c1:/var/www/html/index.html

Luego, accedemos al contenedor c1 a través del navegador usando http://localhost:8080. Si todo está configurado correctamente, deberíamos ver el contenido del archivo index.html.

![26](/Imágenes_png/26.png)

5. Borramos el contenedor c1, para ello invocamos el comando:

>docker rm -f c1

Después, creamos el contenedor c3 con las mismas características que c1, pero sirviendo en el puerto 8081, para ello invocamos el comando:

>docker run -d --name c3 -p 8081:80 -v volumen_web:/var/www/html php:7.4-apache

Luego, accedemos al contenedor c3 a través del navegador usando http://localhost:8080. Si todo está configurado correctamente, deberíamos ver el contenido del archivo index.html.

![27](/Imágenes_png/27.png)

## Bind mount para compartir datos ##
1. Creamos la carpeta y el archivo index.html. Para ello creamos la carpeta llamada saludo y dentro de ella, el archivo index.html con el contenido solicitado. Para ello invocamos el comando:

>mkdir ~/saludo

>`echo "<h1>HOLA SOY OSCAR PABLOS</h1>" > ~/saludo/index.html`

Después arrancamos los contenedores con bind mount. Para ello creamos y arrancamos los dos contenedores basados en la imagen php:7.4-apache, con el bind mount de la carpeta saludo a /var/www/html del contenedor. Uno de ellos usará el puerto 8181 y el otro el puerto 8282. Para el contenedor c1 (puerto 8181), invocamos:

>docker run -d --name c1 -p 8181:80 -v ~/saludo:/var/www/html php:7.4-apache

![28](/Imágenes_png/28.png)

Para el contenedor c2 (puerto 8282), invocamos:

>docker run -d --name c2 -p 8282:80 -v ~/saludo:/var/www/html php:7.4-apache

![29](/Imágenes_png/29.png)
