FROM mysql:8.0
ENV MYSQL_ROOT_PASSWORD="RoboShop@1"
COPY 1-schema.sql  /docker-entrypoint-initdb.d/
COPY 2-app-user.sql  /docker-entrypoint-initdb.d/
COPY 3-master-data.sql  /docker-entrypoint-initdb.d/