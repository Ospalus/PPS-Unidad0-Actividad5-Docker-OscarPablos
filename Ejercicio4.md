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


