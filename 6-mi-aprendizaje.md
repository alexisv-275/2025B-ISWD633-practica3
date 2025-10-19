# MI APRENDIZAJE

## Principales Conceptos Aprendidos

Durante esta práctica profundicé en la gestión de volúmenes y persistencia de datos en Docker, aspectos fundamentales para el manejo de aplicaciones containerizadas en entornos reales:

### 1. **Volúmenes en Docker**
Los volúmenes son el mecanismo principal para persistir datos en Docker. A diferencia del sistema de archivos del contenedor (que es efímero), los volúmenes permiten que la información sobreviva al ciclo de vida del contenedor. 

### 2. **Tipos de Montajes en Docker**
Comprendí las tres formas de persistir datos en contenedores:
- **Bind Mount**: Vincula directorios del host directamente al contenedor, útil para desarrollo.
- **Volumen Nombrado**: Gestionado por Docker, ideal para producción y datos críticos.
- **Volumen Anónimo**: Temporal, se elimina con el contenedor.

### 3. **Persistencia de Datos**
Aprendí que los contenedores son efímeros por naturaleza, y sin volúmenes, todos los datos se pierden al eliminarlos. Los ejercicios con WordPress/MySQL y Drupal/PostgreSQL demostraron cómo los datos persisten incluso después de recrear contenedores.

### 4. **Mountpoint**
Entendí dónde Docker almacena físicamente los volúmenes en el sistema host.

## Tabla Resumen de Comandos Docker

| Comando | Descripción | Ejemplo Aplicado |
|---------|-------------|------------------|
| `docker volume create <nombre>` | Crear un volumen nombrado | `docker volume create vol-postgres` |
| `docker volume ls` | Listar todos los volúmenes | `docker volume ls` |
| `docker volume rm <nombre>` | Eliminar un volumen específico | `docker volume rm vol-postgres` |
| `docker volume prune` | Eliminar volúmenes anónimos sin usar | `docker volume prune` |
| `docker run -v <host>:<contenedor>` | Crear contenedor con bind mount | `docker run -d --name nginx-bind -v .../html:/usr/share/nginx/html nginx:alpine` |
| `docker run -v <volumen>:<contenedor>` | Crear contenedor con volumen nombrado | `docker run -d --name server-postgres -v vol-postgres:/var/lib/postgresql/data postgres` |
| `docker run --mount type=bind,source=<host>,target=<contenedor>` | Sintaxis mount explícita para bind mount | `docker run -d --mount type=bind,source=C:\Users\...\html,target=/usr/share/nginx/html nginx:alpine` |
| `docker run --mount type=volume,src=<vol>,dst=<contenedor>` | Sintaxis mount explícita para volumen | `docker run -d --mount type=volume,src=vol-postgres,dst=/var/lib/postgresql/data postgres` |
| `docker rm -fv <contenedor>` | Eliminar contenedor y su volumen anónimo | `docker rm -fv nginx-bind` |
| `docker inspect <contenedor/volumen>` | Ver información detallada del recurso | `docker inspect vol-postgres` |

## Principales aprendizajes para beneficio de la formación profesional

- **Gestión de datos en producción**: Comprendí la importancia crítica de separar los datos de la aplicación en entornos containerizados, una práctica esencial en DevOps y cloud computing que permite actualizaciones sin pérdida de información.

- **Diseño de arquitecturas resilientes**: Aprendí a diseñar sistemas donde los servicios pueden reiniciarse o actualizarse sin afectar la integridad de los datos, un requisito fundamental en aplicaciones empresariales modernas.

- **Diferenciación de entornos**: Entendí cuándo usar bind mounts (desarrollo local con cambios en tiempo real) versus volúmenes nombrados (producción con datos críticos), optimizando flujos de trabajo según el contexto.

- **Integración de servicios multi-contenedor**: Desarrollé habilidades para orquestar aplicaciones complejas con múltiples componentes (frontend, backend, base de datos) que se comunican entre sí.

- **Troubleshooting y debugging**: Mejoré mi capacidad para diagnosticar problemas de persistencia, conexión entre contenedores y configuración de servicios.
