Iniciar un contenedor
`docker run {NOMBRECONTENEDOR/ID} `

Parar un contenedor
`docker stop {NOMBRECONTENEDOR/ID} ` 

Eliminar un contenedor
`docker rm {NOMBRECONTENEDOR/ID}` 

Eliminar un contenedor forzado
`docker rm  -f {NOMBRECONTENEDOR/ID}` 

Eliminar una imagen
`docker rmi {NOMBREDELAIMAGEN/ID}` 

Ver todos los contenedores activos
`docker ps ` 

Ver todos los contenedores activos y detenidos 
`docker ps -a`

Elinia todos los contenedores detenidos
`docker container prune`

Ver las imagenes descargadas.
`docker images`

*** Una imagen puede tener varios contenedores, la imagen no puede eliminarse hasta eliminar todos los contenedores que la usen ***.

Podemos crear una imagen de docker al crear un archivo Dockerfile. 

Para pasar de un Dockerfile a una imagen es necesario utilizar el comando
Le pasamos la etiqueta -t, que es un tag,  {nombreImagen} nombre que se le asignara a la imagen y un (.) para indicar donde se encuentra ese archivo
`docker build -t ubuntu-new .`


-it para que interactuemos con ese contenedor
-p se utiliza para indicar el puerto interno de nuestra pc y el puerto del contenedor (7070 nuestra pc) (70 el contenedor) 
indicamos el nombre de la imagen 
indicamos el comando, en caso de no indicarlo se va a ejecutar el comando establecido en CMD por defecto que puede ser sobreescrito.
`docker run -it -p 7070:70 ubuntu-new /bin/bash`
Se ejecutara Este es un contendor de ejemplo:
`docker run -it -p 7070:70 ubuntu-new`

-d ejecucion en segundo plano. 

ejecutar un comando en un contenedor 
`docker exec it {nombreContendor} {comando}`

### Diferencia entre cmd y entrypoint 

- EntryPoint: te permite ejecutar un comando no se puede reescribir. Por mas que le pasemos un parametro extra siempre se va a ejecutar lo que pusimos en entrypoint.
- CMD: te permite ejecutar un comando se puede reescribir. Escribiendo  echo y lo que queramos que haga.


### Docker hub
loguearse en dockerhub
`docker login`

subir una imagen a dockerhub:
docker tag {nombre de la imagen a subir } username-dockerhub/nombre-repositorio
`docker tag ubuntu-new juanoxi95/ubuntu-new-repo1`

buscar la imagen en dockerhub:
`docker search juanoxi95/ubuntu-new-repo1 `

bajar una imagen de dockerhub:
`docker pull redis:latest`

### Monitoreo

ver propiedades del contenedor:
`docker inspect {nombredelcontenedor}`

ver los logs del contenedor:
`docker logs -f {nombredelcontenedor}`

ver consumo de recursos del contenedor:
`docker stats {nombredelcontenedor}`

ejecutar comando dentro del contenedor:
`docker exec -it {nombredelcontenedor} {comando}`

### Redes
La red bridge es la utilizada por los contenedores de manera predeterminada cuando no se especifica otra red. Cada contenedor tiene una interfaz de red virtual y los contenedores pueden comunicarse.
La red host permite que un contenedor comparta con la red de la maquina host, el contendor utiliza la red de la computadora. 
Podemos crear nuestra red.

Alistar todas las redes
`docker network ls`

Crear red
`docker network create {nombreRed}`

Ver las propiedades de una red especifica 
`docker network inspect {nombreRed}`

Ejecutar contenedor en una red especifica
`docker run -d --name {nombredelcontenedor}--network {nombredered} {imagen}`
>docker run -d --name my-container-5 --network red-lol nginx:latest

Desconectar contenedor de una red
`docker network disconnect {nombreRed} {nombrecontenedor}`

Eliminar una red
`docker network rm {nombreRed}`


### Volumenes
Permite persistir datos en docker.
Los volumenes es un mecanismo para conservar los datos generados y utilizados por los contenedores docker. Se guardan en un espacio de docker. En entorno de produccion.

Los bind mounts tienen una funcionalidad limitada en comparacion con los volumenes. Cuando se utiliza un montaje de enlace, un archivo o directorio en la maquina host se monta en un contendor.Se guardan en los archivos del sistema. 

crear bind mount en un contenedor (-v), donde se van a guardar los elementos del contenedor:
`docker run -d --name my-mongodb-container -v {"ruta donde se guardan los archivos"} {imagen}`
>docker run -d --name my-mongodb-container -v "/mongodb_data:/data/db" mongo:latest

crear bind mont de un contenedor mysql se le pasa una variable de entorno (-e) 
`docker run --name mysql-cont -v "/mysql_db:/var/lib/mysql" -e MYSQL_ROOT_PASSWORD=1234 -d mysql`
>docker exec -it mysql-cont bash
>mysql -u root -p 1234 

listar volumenes
`docker volume ls `

crear volumen
`docker volume create {nombrevolumen}`

src = volumen que le pasamos al contenedor
dst = carpeta de destino donde se almacena ese volumen
crear un contenedor y asignarle un volumen (--mount src={nombre del volumen} , dst= /data/db {nombre imagen})
El volumen se guarda en docker. es independiente del contenedor.
`docker run -d --name mongocontainer --mount src=mongo_db,dst=/data/db mongo`

El bind mont se guarda local.

### DOCKER COMPOSE 
Docker compose es para crear multiples contendores con estension .yml indicando todos los servicios que vamos a crear. 
Dockerfile crea una imagen.

levantar los servicios de un docker compose
`docker compose up -d`

dar de baja servicios, elimina todos los contenedores.
`docker compose down`

parar un servicio 
`docker compose stop {servicioAParar}`

eliminar un servicio 
`docker compose rm {servicioAParar}`


