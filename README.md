# SistemasOperativos
Afianzar conocimientos de Docher
Camilo Andres Muñoz Muñoz código 2042857
Juan Fernando Calle Sanchez 2127464
William David Hernández solarte 202228934

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
SELECT*FROM pg_tabla

INSERT INTO pg_tabla(mensaje) VALUES(‘hola mundo’); 

\q

docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)
docker network rm pg_network
docker volume rm pg_db
