# Ejercicio 1 #

### Enunciado ###

**Ejercicio para entregar**

Vamos a entregar el ejercicio 4 con algunas modificaciones. Crearemos un contenedor
demonio a partir de la imagen **nginx**, el contenedor se debe llamar **servidor_web** y se debe acceder a él utilizando el puerto **8181** del ordenador donde tengas instalado docker.

Entrega un fichero comprimido o un documento pdf con los siguientes pantallazos:

1. Pantallazo donde se vea la creación del contenedor y podamos comprobar que el
contenedor está funcionando.

2. Pantallazo donde se vea el acceso al servidor web utilizando un navegador web (recuerda que tienes que acceder a la ip del ordenador donde tengas instalado docker)

3. Pantallazo donde se vean las imágenes que tienes en tu registro local.

4. Pantallazo donde se vea como se elimina el contenedor (recuerda que antes debe estar parado el contenedor).


## Desarrollo ##

>1. Pantallazo donde se vea la creación del contenedor y podamos comprobar que el
contenedor está funcionando.

Para la realización de este apartado invocamos el siguiente comando en nuestra máquina de Kali-Linux:


                                docker run -d \
                                --name Oscar_Ceceti \
                                -p 8181:80 \
                                nginx

 ![1](/Imágenes_png/1.png) 

    
**Explicación del comando**

- **docker run**: Ejecuta un nuevo contenedor.
- **-d**: Ejecuta el contenedor en segundo plano (modo demonio).
- **--name Oscar_Ceceti**: Asigna el nombre Oscar_Ceceti al contenedor.
- **-p 8181:80**: Mapea el puerto 8181 del host anfitrión al puerto 80 del  contenedor (el puerto predeterminado de Nginx).
- **nginx**: Utiliza la imagen oficial de Nginx.

Podemos invocar el comando docker ps y verificamos que el contenedor está corriendo:


 ![2](/Imágenes_png/2.png) 

>2. Pantallazo donde se vea el acceso al servidor web utilizando un navegador web (recuerda que tienes que acceder a la ip del ordenador donde tengas instalado docker)

Accedemos al servidor desde Firefox en la dirección **http://localhost:8181** donde veremos la página de bienvenida de **nginx:**


 ![3](/Imágenes_png/3.png) 

 >3. Pantallazo donde se vean las imágenes que tienes en tu registro local.

Para la realización de este apartado, tendremos que invocar el comando **docker images**

 ![4](/Imágenes_png/4.png) 

 En la imagen tenemos varios campos de impormación, **TAG** o etiqueta que por defecto muestra latest (la última), **IMAGE ID** que muestra la id de la imagen, **CREATED** que muestra la información de cuando se creó la imagen y **SIZE** que muestra el tamaño de la imagen.

 >4. Pantallazo donde se vea como se elimina el contenedor (recuerda que antes debe estar parado el contenedor).

 Para eliminar el contenedor, primero tenemos que pararlo invocando el comando **docker stop** y id del contenedor. Primero invocamos **docker ps** para ver el id, después invocamos **docker stop 97dd069155f4** 

  ![5](/Imágenes_png/5.png) 

  Y una vez parado, ya podríamos eliminarlo invocando el comando **docker rm** y el id del contenedor, en este caso **97dd069155f4**

  ![6](/Imágenes_png/6.png) 

Y después invocamos **docker ps** para verificar que no hay ningún contenedor corriendo:

  ![7](/Imágenes_png/7.png) 



<p align="center">
          <img src="/Imágenes_png/6.png" alt="">
        </p>
