## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO
```
docker network create net-wp -d bridge
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
La carpeta db del host contiene todos los archivos de datos generados por el contenedor de MySQL.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
```
docker run -d --name mysql-wp \
  --network net-wp \
  -v /mnt/c/Users/USER/Documents/ejercicio3/db:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=admin123 \
  -e MYSQL_DATABASE=wordpress \
  -e MYSQL_USER=wpuser \
  -e MYSQL_PASSWORD=wpsecret \
  mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
La carpeta db, que al principio estaba vacía, ahora contiene varios archivos y subcarpetas generados automáticamente por MySQL.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
```
docker run -d --name wordpress-wp \
  --network net-wp \
  -p 9500:80 \
  -v /mnt/c/Users/USER/Documents/ejercicio3/www:/var/www/html \
  -e WORDPRESS_DB_HOST=mysql-wp \
  -e WORDPRESS_DB_USER=wpuser \
  -e WORDPRESS_DB_PASSWORD=wpsecret \
  -e WORDPRESS_DB_NAME=wordpress \
  wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada
<img width="929" height="657" alt="image" src="https://github.com/user-attachments/assets/38774ce2-8679-4139-850b-4f3d99d16b19" />


### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
Cuando el contenedor de WordPress se elimina y se vuelve a crear manteniendo los volúmenes montados (.../ejercicio3/www para WordPress y .../ejercicio3/db o el volumen de Docker para MySQL), la información del sitio y la base de datos persisten.

