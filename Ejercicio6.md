# Ejercicio 6 #

### Enunciado 

### Ejercicio para entregar

Para la realización de estos ejercicios es necesario tener una cuenta en Docker Hub.

Entrega uno de estos dos ejercicios (si estás muy aburrido puedes entregar los dos):

**Creación de una imagen a partir de un contenedor**

1. Arranca un contenedor desde una imagen base debian o ubuntu.
2. Instala los paquetes inetutils-ping, iproute2 y dnsutils con distintas herramientas de redes.
3. Crea una imagen a partir de este contenedor (recuerda que tienes que utilizar el nombre de tu usuario Docker Hub). La imagen se debe llamar <tu_usuario_docker_hub>/comandos_redes.
4. Sube la imagen a Docker Hub.
5. Descarga la imagen en otro ordenador donde tengas docker instalado, y crea un contenedor a partir de ella. (Si no tienes otro ordenador con docker instalado, borra la imagen en tu ordenador y bájala de Docker Hub).

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se vea la creación del contenedor.
- Pantallazo donde se vea el comando que crea la nueva imagen.
- Pantallazo donde se vea la imagen subida a tu cuenta de Docker Hub.
- Pantallazo donde se vea la bajada de la imagen y la creación de un nuevo contenedor.

**Creación de una imagen a partir de un Dockerfile**

1. Crea una página web estática (por ejemplo busca una plantilla HTML5). O simplemente crea un index.html.
2. Crea un fichero Dockerfile que permita crear una imagen con un servidor web sirviendo la página. Puedes usar una imagen base debian o ubuntu, o una imagen que tenga ya un servicio web, como hemos visto en el apartado Ejemplo 1: Construcción de imágenes con una página estática.
3. Ejecuta el comando docker que crea la nueva imagen. La imagen se debe llamar <tu_usuario_docker_hub>/mi_servidor_web.
4. Conéctate a Docker Hub y sube la imagen que acabas de crear.
5. Descarga la imagen en otro ordenador donde tengas docker instalado, y crea un contenedor a partir de ella. (Si no tienes otro ordenador con docker instalado, borra la imagen en tu ordenador y bájala de Docker Hub).

Deberás entregar los siguientes pantallazos comprimidos en un zip o en un documento pdf:

- Pantallazo donde se vea el contenido del fichero Dockerfile.
- Pantallazo donde se vea el comando que crea la nueva imagen.
- Pantallazo donde se vea la imagen subida a tu cuenta de Docker Hub.
- Pantallazo donde se vea la bajada de la imagen y la creación de un nuevo contenedor.

## Resultados

**Creación de una imagen a partir de un contenedor**

1. Para arrancar un contenedor desde una imagen base debian o ubuntu invocamos el siguiente comando:

>docker run -it --name red-tools ubuntu

![49](/Imágenes_png/49.png)

2. Ahora  instalamos los paquetes inetutils-ping, iproute2 y dnsutils con distintas herramientas de redes. Para ello invocamos los comandos:

>apt update

![50](/Imágenes_png/50.png)

>apt install -y inetutils-ping iproute2 dnsutils

![51](/Imágenes_png/51.png)

3. Creamos una imagen a partir del contenedor 

>docker commit red-tools ospalus/comandos_redes

![52](/Imágenes_png/52.png)

4. Subimos la imagen a Docker Hub.

Aquí hemos tenido problemas al poner el password pero hemos creado un token con permisos de lectura y escritura en la web de Docker Hub para realizar este apartado. Primero tenemos que hacer login:

![53](/Imágenes_png/53.png)

Después invocamos:

>docker push ospalus/comandos_redes

![54](/Imágenes_png/54.png)


Como no tenemos otra máquina con docker instalado, vamos a borrar la imagen y la volvemos a descargar de Docker Hub. Para borrar la imagen invocamos el comando:

>docker rmi ospalus/comandos_redes

![55](/Imágenes_png/55.png)

Y tenemos que volver a descargar la imagen que hemos subido. Para ello invocamos:

>docker pull ospalus/comandos_redes

![55](/Imágenes_png/56.png)

