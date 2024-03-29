# Docker-Compose example

This docker-compose file will run a spring boot app, mysql and phpmyadmin container together.

## Docker Compose File

```
version: '3.3'

services:
    db:
      image: mysql:latest
      container_name: mysql-db2   
      environment:
        - MYSQL_ROOT_PASSWORD=mukit
        - MYSQL_USER=root
      ports:
        - "3306:3306"
      restart: always

    phpmyadmin:
      image: phpmyadmin/phpmyadmin:latest
      container_name: my-php-myadmin
      ports:
        - "8082:80"
      restart: always
        
      depends_on:
        - db
      environment:
        SPRING_DATASOURCE_USERNAME: root
        SPRING_DATASOURCE_PASSWORD: mukit
        
    customerservice:
      image: customer-service2
      container_name: customer-container  
      build:
        context: .
        dockerfile: Dockerfile
      ports:
        - "8084:8084"
      restart: always
        
      depends_on:
        - db
      environment:
        SPRING_DATASOURCE_URL: jdbc:mysql://mysql-db2:3306/customer?createDatabaseIfNotExist=true
        SPRING_DATASOURCE_USERNAME: root
        SPRING_DATASOURCE_PASSWORD: mukit
```


## Description