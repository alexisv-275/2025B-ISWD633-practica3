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
docker run -d --name nginx-bind -P -v C:\Users\Alexisis\Documents\nginx\html:/usr/share/nginx/html nginx:alpine
```

Dado que se mapearon todos los puertos es necesario verificar qué puerto se asigno al host para acceder al servidor mediante: 

```
docker ps
```

<img width="929" height="133" alt="image" src="https://github.com/user-attachments/assets/8cf7457f-8bee-48aa-9b86-166bf1a9a060" />


### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Al ingresar al servidor de nginx aparece el mensaje 403, que significa que el recurso al que se quizo acceder no existe, en este caso es porque la carpeta html está vacía y no existe el archivo index.html.

<img width="888" height="490" alt="image" src="https://github.com/user-attachments/assets/2ee45523-fe28-40b7-b352-425fc06eddd6" />

### ¿Qué pasa con el archivo index.html del contenedor?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El archivo index.html original del contenedor es reemplazado/oculto por el contenido de la carpeta del host (que está vacía). El bind mount sobrescribe el contenido del directorio del contenedor.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Ahora se muestra el template HTML5 descargado, ya que el archivo index.html y todos los recursos están disponibles en la carpeta html del host, que está montada en el contenedor.

<img width="949" height="1034" alt="image" src="https://github.com/user-attachments/assets/c771323e-f05f-4b5a-9c82-bcf4d2aee270" />

### Eliminar el contenedor
# COMPLETAR CON EL COMANDO
```
docker rm -f nginx-bind
```
### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Se carga el recurso que se había creado en el anterior contenedor dado que al haber definido la misma ruta del bind-mount, los datos persisten. 

<img width="933" height="1004" alt="image" src="https://github.com/user-attachments/assets/5a769d26-8286-45ef-9526-c06a935fa33e" />


