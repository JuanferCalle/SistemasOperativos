# SistemasOperativos
Afianzar conocimientos de Docher
Camilo Andres Muñoz Muñoz código 2042857
Juan Fernando Calle Sanchez 2127464
William David Hernández solarte 202228934

Pasos para la Tarea del Sistema Operativo:

En primer lugar, procedemos a crear el volumen al que asignaremos pg_server:
docker volume create pg_db

Luego, creamos la red que conectará al cliente y al servidor:
docker network create pg_network

A continuación, creamos pg_server:
docker run --name pg_server --network pg_network -v pg_db:/var/lib/postgresql/data -e POSTGRES_PASSWORD=contrasena -d postgres:15-bookworm

Nota: Para verificar si el servidor está funcionando correctamente, usar "docker logs pg_server". Recuerda que puede dar error si es incompatible con la versión 15-bookworm.

Después, creamos la base de datos dentro de pg_server de esta manera:

docker exec -it pg_server bash -> para acceder a la consola de comandos del contenedor

psql -U postgres -> para entrar a postgres

Una vez dentro:

CREATE DATABASE tarea_db;

\c tarea_db

CREATE TABLE pg_tabla(
id SERIAL PRIMARY KEY,
mensaje TEXT
);

\q

exit

Ahora creamos el cliente y abrimos la terminal del contenedor:

docker run --name pg_client --network pg_network -it postgres:15-bookworm psql -h pg_server -U postgres

Introducir la contraseña asignada al servidor, en este caso "contrasena".

Dentro del cliente, ejecutamos:

\c tarea_db

SELECT * FROM pg_tabla

Luego, seguimos los pasos indicados en la validación:

Para verificar que todo funciona según lo representado en la gráfica:

Ejecutar el contenedor de la base de datos por primera vez utilizando la versión de Postgres 15-bookworm para mostrar que la base de datos ha sido creada.
Insertar un registro en la base de datos con el mensaje 'hola mundo'.
Para salir, utilizamos \q

Detenemos la ejecución del contenedor que corre la versión Postgres 15-bookworm:

docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)

Ahora ejecutamos el cliente y dentro de este contenedor realizamos lo siguiente:

Borrar los contenedores (pg_server, pg_client), el volumen (pg_db) y la red (pg_network) creados para esta tarea.

Para borrar:

docker network rm pg_network

docker volume rm pg_db



docker volume create pg_db

docker network create pg_network

docker run --name pg_server --network pg_network -v pg_db:/var/lib/postgresql/data -e POSTGRES_PASSWORD=contrasena -d postgres:15-bookworm

docker exec -it pg_server bash

psql -U postgres

CREATE DATABASE tarea_db;
\c tarea_db
;CREATE TABLE pg_tabla(
    id SERIAL PRIMARY KEY,
    mensaje TEXT
); 
\q
exit

docker run - - name pg_client - -network pg_network -it postgres:15-bookworm psql -h pg_server -U postgres

 \c tarea_db
SELECT*FROM pg_tabla

 INSERT INTO pg_tabla(mensaje) VALUES(‘hola mundo’);
\q

docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)

docker network rm pg_network
docker volume rm pg_db

