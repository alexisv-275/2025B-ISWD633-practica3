## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
```
docker network create net-wp
```

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Inicialmente la carpeta db está vacía, no contiene ningún archivo.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO
```
docker run -d --name servidor-mysql --network net-wp -v C:\Users\Alexisis\Documents\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wordpress_user -e MYSQL_PASSWORD=wordpress_pass mysql:8
```

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Ahora contiene todos los archivos relacionados al contenedor creado con la imagen de mysql. 

<img width="846" height="919" alt="image" src="https://github.com/user-attachments/assets/1e3fa370-c0d1-41b6-ae4f-04a3a0ca0beb" />

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html
Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
```
docker run -d --name servidor-wordpress --network net-wp -p 9500:80 -v C:\Users\Alexisis\Documents\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=servidor-mysql -e WORDPRESS_DB_USER=wordpress_user -e WORDPRESS_DB_PASSWORD=wordpress_pass -e WORDPRESS_DB_NAME=wordpress_db wordpress
```

### Personalizar la apariencia de wordpress y agregar una entrada

<img width="1832" height="1120" alt="image" src="https://github.com/user-attachments/assets/416038bf-255e-411f-bec7-16e274289d0d" />

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
```
docker rm -f servidor-wordpress
```
<img width="605" height="69" alt="image" src="https://github.com/user-attachments/assets/6847947f-ba7b-4b1c-8b37-3c1269440264" />


# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 
La entrada (post) creada en el anterior contenedor persiste dado que se le asigno la misma ruta del bind-mount, que no se modificó o borró y se almacenó en el host. 
