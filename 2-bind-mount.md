# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
```
docker run -d --name nginx-bind \
  -p 8080:80 \
  -v /mnt/c/Users/USER/Documents/nginx/html:/usr/share/nginx/html \
  nginx:alpine
```

### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Al ingresar a la ruta de localhost:8080 en el navegador sale un error de tipo 403, 403 Forbidden


### ¿Qué pasa con el archivo index.html del contenedor?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Cuando se crea el contenedor usando un bind mount, el directorio del host (nginx/html) reemplaza completamente el contenido del directorio /usr/share/nginx/html dentro del contenedor. Los archivos originales del contenedor (incluido el index.html por defecto de Nginx) ya no existen dentro del contenedor. En su lugar, Nginx intenta acceder al contenido de la carpeta vacía del host.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Al ingresar a http://localhost:8080, el servidor Nginx muestra el template HTML descargado desde HTML5 UP, lo que confirma que está sirviendo el contenido directamente desde el directorio local del host.

### Eliminar el contenedor
# COMPLETAR CON EL COMANDO
```
docker rm -f nginx-bind
```

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El servidor mantiene y muestra exactamente el mismo contenido del template sin necesidad de volver a copiar los archivos, ya que los datos se encuentran almacenados fuera del contenedor, en el directorio del host.
