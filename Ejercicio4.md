# Ejercicio 4 #

### Enunciado ##

### Ejercicio para entregar

Entrega uno de estos dos ejercicios (si estás muy aburrido puedes entregar los dos):

### Trabajar con redes docker ###

1. Vamos a crear dos redes de ese tipo (BRIDGE) con los siguientes datos:

**Red1**

- Nombre: red1
- Dirección de red: 172.28.0.0
- Máscara de red: 255.255.0.0
- Gateway: 172.28.0.1

**Red2**

- Nombre: red2
- Es resto de los datos será proporcionados automáticamente por Docker.

2. Poner en ejecución un contenedor de la imagen ubuntu:20.04 que tenga como hostname host1, como IP 172.28.0.10 y que esté conectado a la red1. Lo llamaremos u1.
3. Entrar en ese contenedor e instalar la aplicación ping (apt update && apt install inetutils-ping).
4. Poner en ejecución un contenedor de la imagen ubuntu:20.04 que tenga como hostname host2 y que esté conectado a la red2. En este caso será docker el que le de una IP correspondiente a esa red. Lo llamaremos u2.
5. Entrar en ese contenedor e instalar la aplicación ping (apt update && apt install inetutils-ping).

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se vea la configuración de red del contenedor u1.
- Pantallazo donde se vea la configuración de red del contenedor u2.
- Pantallazo donde desde cualquiera de los dos contenedores se pueda ver que no podemos hacer ping al otro ni por ip ni por nombre.
- Pantallazo donde se pueda comprobar que si conectamos el contenedor u1 a la red2 (con docker network connect), desde el contenedor u1, tenemos acceso al contenedor u2 mediante ping, tanto por nombre como por ip.

### Despliegue de Nextcloud + mariadb/postgreSQL ###

Vamos a desplegar la aplicación nextcloud con una base de datos (puedes elegir mariadb o PostgreSQL) **(NOTA: Para que no te de errores utiiliza la imagen mariadb:10.5)**. Te puede servir el ejercicio que hemos realizado para desplegar *Wordpress*. Para ello sigue los siguientes pasos:

1. Crea una red de tipo bridge.
2. Crea el contenedor de la base de datos conectado a la red que has creado. La base de datos se debe configurar para crear una base de dato y un usuario. Además el contenedor debe utilizar almacenamiento (volúmenes o bind mount) para guardar la información. Puedes seguir la documentación de mariadb o la de PostgreSQL.
3. A continuación, siguiendo la documentación de la imagen nextcloud, crea un contenedor conectado a la misma red, e indica las variables adecuadas para que se configure de forma adecuada y realice la conexión a la base de datos. El contenedor también debe ser persistente usando almacenamiento.
4. Accede a la aplicación usando un navegador web.
Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo con la instrucción para crear el contenedor de la base de datos.
- Pantallazo con la instrucción para crear el contenedor de la aplicación.
- Pantallazo donde se ve el acceso a la aplicación desde un navegador web.

## Resultados
### Trabajar con redes docker
1. Vamos a crear las redes socilitadas con una dirección específica. Para la **red1** invocamos:

>docker network create --subnet=172.28.0.0/16 --gateway=172.28.0.1 red1

Creamos también la **red2**:

>docker network create red2

Tendriámos un resultado así:

![33](/Imágenes_png/33.png)

Ahora vamos a crear y ejecutar el contenedor **u1** en la **red1**, para ello invocamos el comando:

>docker run -d --name u1 --hostname host1 --net red1 --ip 172.28.0.10 ubuntu:20.04 sleep infinity


![34](/Imágenes_png/34.png)

Después accedemos al contenedor **u1** e instalamos *ping*:

>docker exec -it u1 bash

>apt update && apt install -y inetutils-ping iproute2

![36](/Imágenes_png/36.png)

Después, creamos y ejecutamos el contenedor **u2** en la **red2** (Docker asignará la IP automáticamente):

>docker run -d --name u2 --hostname host2 --net red2 ubuntu:20.04 sleep infinity

![35](/Imágenes_png/35.png)

Después accedemos al contenedor **u2** e instalamos *ping*:

>docker exec -it u2 bash

>apt update && apt install -y inetutils-ping iproute2


![37](/Imágenes_png/37.png)

Vamos ahora con los pantallazos pedidos. Pantallazo donde se vea la configuración de red del contenedor u1:

>docker exec -it u1 bash

>ip a

![38](/Imágenes_png/38.png)

Pantallazo donde se vea la configuración de red del contenedor u2:

>docker exec -it u2 bash

>ip a

![39](/Imágenes_png/39.png)

El ejercicio nos pide un pantallazo donde no podamos hacer ping entre los contenedores mientras que no los conectemos. Hacer ping es imposible porque están en redes diferentes pero aun así, vamos a intentarlo:

![41](/Imágenes_png/41.png)

No podemos hacer ping. Para poder hacer ping, tenemos que conectar los contenedores porque se encuentran en redes diferentes, para ello invocamos 

>docker network connect red2 u1

Después entramos en el contenedor u1 y hacemos ping al host2:

![40](/Imágenes_png/40.png)


### Despliegue de Nextcloud + mariadb/postgreSQL

1. Crear la red de tipo bridge
Primero, creamos una red de tipo bridge para que ambos contenedores (el de la base de datos y el de Nextcloud) puedan comunicarse entre sí. Para ello invocamos:

>docker network create --driver bridge nextcloud_network

![42](/Imágenes_png/42.png)


2. Creamos el contenedor de MariaDB

Usaremos la imagen mariadb:10.5 para crear el contenedor de la base de datos. Especificamos la red creada y las variables de entorno necesarias (como el nombre de la base de datos, el usuario y la contraseña). Además, utilizamos un volumen para persistir los datos.

>docker run -d --name mariadb \
  --network nextcloud_network \
  -e MYSQL_ROOT_PASSWORD=root_password \
  -e MYSQL_DATABASE=nextcloud \
  -e MYSQL_USER=nextcloud_user \
  -e MYSQL_PASSWORD=nextcloud_password \
  -v mariadb_data:/var/lib/mysql \
  mariadb:10.5

**Explicación de comandos:**

- MYSQL_ROOT_PASSWORD: La contraseña del usuario root de la base de datos.
- MYSQL_DATABASE: El nombre de la base de datos que se creará.
- MYSQL_USER: El nombre del usuario de la base de datos.
- MYSQL_PASSWORD: La contraseña del usuario de la base de datos.
- mariadb_data: Volumen de Docker que persistirá los datos de la base de datos.

![43](/Imágenes_png/43.png)


3. Creamos el contenedor de Nextcloud

Luego, creamos el contenedor de Nextcloud y lo conectamos a la misma red. Se deben proporcionar las variables de entorno necesarias para que Nextcloud pueda conectarse a la base de datos de MariaDB.

>docker run -d --name nextcloud \
  --network nextcloud_network \
  -e MYSQL_PASSWORD=nextcloud_password \
  -e MYSQL_DATABASE=nextcloud \
  -e MYSQL_USER=nextcloud_user \
  -e MYSQL_HOST=mariadb \
  -v nextcloud_data:/var/www/html \
  -p 8080:80 \
  nextcloud

**Explicación de comandos:**

- MYSQL_PASSWORD: La contraseña del usuario de la base de datos (debe coincidir con la de la creación de MariaDB).
- MYSQL_DATABASE: El nombre de la base de datos que Nextcloud usará (debe coincidir con el nombre de la base de datos en MariaDB).
- MYSQL_USER: El nombre de usuario para la base de datos.
- MYSQL_HOST: El nombre del contenedor de la base de datos (mariadb en este caso).
nextcloud_data: Volumen de Docker que persistirá los datos de Nextcloud.
- -p 8080:80: Exponer Nextcloud en el puerto 8080 de tu máquina local.

![44](/Imágenes_png/44.png)

4. Acceder a la aplicación desde un navegador web

Una vez que ambos contenedores estén en funcionamiento, puedes acceder a Nextcloud desde tu navegador utilizando la dirección http://localhost:8080 

Y el resultado es este:

![45](/Imágenes_png/45.png)

