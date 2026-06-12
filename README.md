# Taller Práctico de Docker

## Estudiante

Sofía Giraldo

## Objetivo

El objetivo de este taller fue aprender los conceptos fundamentales de Docker mediante la creación y administración de contenedores, el uso de imágenes, la persistencia de datos con volúmenes y la construcción de una imagen personalizada utilizando un Dockerfile.

---

# Parte 1 - Verificación de instalación

Se verificó la instalación de Docker y Docker Compose mediante los siguientes comandos:


docker --version
docker compose version


Resultado: se confirmó que Docker y Docker Compose se encontraban correctamente instalados y funcionando.

---

# Parte 2 - Primer contenedor

Se ejecutó el siguiente comando:


docker run hello-world


Resultado: Docker descargó automáticamente la imagen desde Docker Hub y mostró un mensaje de bienvenida confirmando que la instalación funciona correctamente.

---

# Parte 3 - Contenedor interactivo

Se creó un contenedor Ubuntu en modo interactivo:


docker run -it ubuntu bash


Dentro del contenedor se ejecutaron los comandos:


ls
cat /etc/os-release


Resultado: se visualizaron los archivos del sistema y la información del sistema operativo Ubuntu.

---

# Parte 4 - Visualización de contenedores

Se utilizaron los comandos:


docker ps
docker ps -a


Resultado: se visualizaron los contenedores activos y los contenedores detenidos, identificando su estado, imagen utilizada y nombre asignado.

---

# Parte 5 - Despliegue de un servidor web

Se creó un contenedor basado en Nginx:


docker run -d --name servidor-web -p 8080:80 nginx


Resultado: se accedió correctamente al servidor web desde el navegador mediante la dirección:


http://localhost:8080


mostrando la página de bienvenida de Nginx.

---

# Parte 6 - Ciclo de vida de contenedores

Se realizaron operaciones de administración sobre el contenedor:

docker stop servidor-web
docker start servidor-web
docker restart servidor-web
docker logs servidor-web
docker logs -f servidor-web


Resultado: se comprobó el funcionamiento de las acciones de detener, iniciar, reiniciar y monitorear contenedores.

---

# Parte 7 - Acceso y modificación de un contenedor

Se ingresó al contenedor en ejecución:


docker exec -it servidor-web sh


Posteriormente se modificó el archivo principal de la página web:


echo "<h1>Modificado desde dentro del contenedor</h1>" > /usr/share/nginx/html/index.html


Resultado: la página web mostró el contenido personalizado al actualizar el navegador.

---

# Parte 8 - Ejecución de múltiples contenedores

Se desplegaron tres contenedores independientes utilizando la misma imagen Nginx:


docker run -d --name web-1 -p 8081:80 nginx
docker run -d --name web-2 -p 8082:80 nginx
docker run -d --name web-3 -p 8083:80 nginx


Resultado: se comprobó que múltiples contenedores pueden ejecutarse simultáneamente utilizando la misma imagen, manteniendo independencia entre ellos.

---

# Parte 9 - Base de datos sin persistencia

Se desplegó una instancia de MariaDB:


docker run -d --name mi-db -e MYSQL_ROOT_PASSWORD=secret123 -e MYSQL_DATABASE=taller -p 3306:3306 mariadb:11


Se creó una tabla llamada `productos` y se insertaron registros de prueba.

Posteriormente el contenedor fue eliminado y recreado.

Resultado: los datos desaparecieron, demostrando que los datos almacenados dentro del contenedor se pierden cuando este es eliminado.

---

# Parte 10 - Persistencia mediante volúmenes

Se creó una nueva instancia de MariaDB utilizando un volumen Docker:


docker run -d --name mi-db -e MYSQL_ROOT_PASSWORD=secret123 -e MYSQL_DATABASE=taller -v datos-mariadb:/var/lib/mysql -p 3306:3306 mariadb:11


Resultado: después de eliminar y recrear el contenedor, los datos permanecieron almacenados gracias al volumen, demostrando la persistencia de la información.

---

# Parte 11 - Construcción de una imagen personalizada

Se creó una carpeta de trabajo con los siguientes archivos:

## index.html

```html
<h1>Imagen construida por mi</h1>
```

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

Posteriormente se construyó la imagen:


docker build -t mi-imagen:v1 .


Se verificó la creación de la imagen mediante:


docker images


Finalmente se creó un contenedor utilizando la imagen personalizada:


docker run -d --name mi-contenedor -p 9090:80 mi-imagen:v1


Resultado: al acceder a:


http://localhost:9090


se visualizó correctamente la página personalizada definida en el archivo `index.html`.

---

# Conclusiones

Durante el desarrollo del taller se adquirieron conocimientos fundamentales sobre Docker, incluyendo:

* Uso de imágenes y contenedores.
* Administración del ciclo de vida de contenedores.
* Exposición de servicios mediante puertos.
* Uso de registros y monitoreo.
* Persistencia de datos mediante volúmenes.
* Creación de imágenes personalizadas con Dockerfile.
* Despliegue de aplicaciones web dentro de contenedores.

Estas actividades permitieron comprender el funcionamiento básico de la tecnología de contenedores y su utilidad para el despliegue y administración de aplicaciones.
