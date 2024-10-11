# Microservicios NestJS con Docker

Este proyecto contiene una arquitectura de microservicios desarrollada con NestJS y orquestada con Docker Compose. Incluye un gateway de cliente y varios microservicios.

## Requisitos Previos

- Docker
- Node.js (para desarrollo local)

## Configuración

1. Asegúrate de tener un archivo `.env` en la raíz del proyecto. Este archivo es utilizado por el `docker-compose.yml` para configurar las variables de entorno.

2. Verifica que todos los servicios estén correctamente configurados en el `docker-compose.yml`.


### Pasos para crear los Git Submodules


1. Crear un nuevo repositorio en GitHub
2. Clonar el repositorio en la máquina local
3. Añadir el submodule, donde `repository_url` es la url del repositorio y `directory_name` es el nombre de la carpeta donde quieres que se guarde el sub-módulo (no debe de existir en el proyecto)
```
git submodule add <repository_url> <directory_name>
```
4. Añadir los cambios al repositorio (git add, git commit, git push)
Ej:
```
git add .
git commit -m "Add submodule"
git push
```
5. Inicializar y actualizar Sub-módulos, cuando alguien clona el repositorio por primera vez, debe de ejecutar el siguiente comando para inicializar y actualizar los sub-módulos
```
git submodule update --init --recursive
```
6. Para actualizar las referencias de los sub-módulos
```
git submodule update --remote
```


## Importante
Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal. 

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.



## Instrucciones de Inicio

Para levantar todos los servicios (gateway y microservicios), sigue estos pasos:

1. Abre una terminal en la raíz del proyecto.

2. Ejecuta el siguiente comando para construir e iniciar todos los contenedores:

   ```
   docker compose up -d --build
   ```

   Este comando hará lo siguiente:

   - Construirá las imágenes de Docker si no existen o si ha habido cambios.
   - Iniciará todos los servicios definidos en el `docker-compose.yml`.
   - Ejecutará los contenedores en modo detached (`-d`).

3. Espera a que todos los servicios estén en funcionamiento. Puedes verificar el estado con:

   ```
   docker compose ps
   ```

## Orden de Inicio de Servicios

Docker Compose se encargará de manejar las dependencias entre servicios según lo definido en el archivo `docker-compose.yml`. Sin embargo, ten en cuenta que:

1. Las bases de datos y servicios de mensaje (como RabbitMQ) generalmente se inician primero.
2. Los microservicios se iniciarán después.
3. El gateway del cliente será el último en estar completamente operativo, ya que depende de los microservicios.

## Detener los Servicios

Para detener los contenedores sin eliminarlos:

```
docker compose stop
```

## Desarrollo Local

Para desarrollo local fuera de Docker:

1. Instala las dependencias en cada servicio:

   ```
   cd [directorio-del-servicio]
   npm install
   ```

2. Crea un archivo `.env.local` con las configuraciones para desarrollo local.

3. Inicia cada servicio individualmente:

   ```
   npm run start:dev
   ```

## Notas Adicionales

- Asegúrate de que los puertos necesarios estén libres en tu máquina local.
- Si realizas cambios en el código, deberás reconstruir los contenedores con `docker compose up -d --build`.
- Para añadir nuevos servicios, actualiza el `docker-compose.yml` y crea los Dockerfiles correspondientes.

## Solución de Problemas

Si encuentras problemas al construir o iniciar los contenedores:

1. Verifica la conectividad a Internet para la descarga de paquetes npm.
2. Asegúrate de que no haya conflictos de puertos.
3. Revisa los logs de Docker para identificar errores específicos.

Para más ayuda, consulta la documentación de Docker y NestJS, o contacta a emanuel brou :D.
