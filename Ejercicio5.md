# Ejercicio 5 #

### Enunciado 

### Ejercicio para entregar

Entrega uno de estos dos ejercicios (si estás muy aburrido puedes entregar los dos):

## Despliegue de prestashop 

Es esta tarea vamos a desplegar una tienda virtual construída con prestashop. Utilizaremos el fichero docker-compose.yml de Bitnami que podemos encontrar en la siguiente URL.

Una vez hemos descargado el fichero docker-compose.yml asociado deberemos modificarlo de la siguiente manera:

Modificar los valores de las variables de entorno para conseguir lo siguiente:

1. El usuario de prestashop para conectarse a la base de datos deberá ser pepe y su contraseña pepe. Investigar en la página de Dockerhub cuál es el nombre de las variables de entorno que debo modificar y/o añadir.
2. Modificar el nombre de la base de datos de prestashop para que se llame mitienda. Debéis de modificar esos valores en los dos servicios. Investigar en la página de Dockerhub cuál es el nombre de las variables de entorno que debo modificar.
3. Ten en cuenta que si tienes instalado docker en una máquina virtual y tienes que poner la IP de la máquina para acceder a los contenedores, debes modificar la variable de entorno PRESTASHOP_HOST para poner esa dirección ip.
4. Por último, si tienes que repetir el ejercicio, borra el escenario con docker-compose down -v, para eliminar los volúmenes y que la modificación de la configuración se tenga en cuenta.

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se vea el fichero docker-compose.yml modificado.
- Pantallazo donde se vea los contenedores funcionando con la instrucción docker-compose.
- Pantallazo donde se vea el acceso desde el navegador a la aplicación.

## Despliegue de Nextcloud

Vamos a desplegar la aplicación nextcloud con una base de datos (puedes elegir mariadb o PostgreSQL) utilizando la aplicación docker-compose. Puedes coger cómo modelo el fichero docker-compose.yml el que hemos estudiado para desplegar WordPress.

1. Instala docker-compose en tu ordenador.
2. Dentro de un directorio crea un fichero docker-compose.yml para realizar el despliegue de nextcloud con una base de datos. Recuerda las variables de entorno y la persistencia de información.
3. Levanta el escenario con docker-compose.
4. Muestra los contenedores con docker-compose.
5. Accede a la aplicación y comprueba que funciona.
6. Comprueba el almacenamiento que has definido y que se ha creado una nueva red de tipo bridge.
7. Borra el escenario con docker-compose.

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se vea el fichero docker-compose.yaml.
- Pantallazo donde se vea los contenedores funcionando con la instrucción docker-compose.
- Pantallazo donde se vea el acceso desde el navegador a la aplicación.

## Resultados

### Despliegue de Nextcloud

1. Tenemos ya docker-compose instalado. Ahora creamos el archivo *docker-compose.yml* y agregamos lo siguiente:

![46](/Imágenes_png/46.png)

Después levantamos el escenario invocando:

>docker-compose up -d

Y para ver si todo va bien, invocamos:

>docker-compose ps

![47](/Imágenes_png/47.png)

Y vemos que todos los servicios están levantados y corriendo perfectamente. Ahora nos vamos al navegador a la dirección http://localhost:8080/ y deberíamos ver lo siguiente:

![48](/Imágenes_png/48.png)

