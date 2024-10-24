# Microservicios NestJS con Docker

Este proyecto contiene una arquitectura de microservicios desarrollada con NestJS y orquestada con Docker Compose. Incluye un gateway de cliente y varios microservicios.

## error postgress

sudo chmod -R 775 /home/emanuel/proyectos/microservicios_nestjs/03-products-launcher/orders-ms/

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

3. Espera a que todos los servicios estén en funcionamiento. Puedes verificar el estado con:

   ```
   docker compose ps
   ```

## PASOS PROD

1. clonar el repositorio
2. Crear un .env basado en el .env.template
3. Ejecutar el comando
   ```
   docker compose -f docker-compose.prod.yml build
   ```