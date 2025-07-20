FROM mysql:8.0
ENV MYSQL_ROOT_PASSWORD="RoboShop@1"
COPY 01-schema.sql  /docker-entrypoint-initdb.d/
COPY 02-app-user.sql  /docker-entrypoint-initdb.d/
COPY 03-master-data.sql  /docker-entrypoint-initdb.d/