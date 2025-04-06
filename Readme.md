# MySQL and phpMyAdmin Setup with Docker Compose

## Docker compose file
Create `docker-compose.yml` file in current directory before running containers
```yml
services:
  mysql:
    image: mysql:latest  
    container_name: mysql-container
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword  
      MYSQL_DATABASE: exampledb          
      MYSQL_USER: user                   
      MYSQL_PASSWORD: userpassword       
    ports:
      - "3306:3306"  
    volumes:
      - mysql-data:/var/lib/mysql

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin-container
    environment:
      PMA_HOST: mysql
      PMA_USER: user
      PMA_PASSWORD: userpassword
    ports:
      - "8080:80"

volumes:
  mysql-data:
    driver: local
```
## Fixing Permission Issues
If you encounter permission issues with Docker, run the following commands:

```sh
sudo usermod -aG docker $USER
newgrp docker
```

---

## Managing Containers

### Remove Containers
To stop and remove all containers, networks, and volumes created by Docker Compose:

```sh
docker compose down
```

### Start Containers
To start the containers in detached mode:

```sh
docker compose up -d
```

---

## Accessing the MySQL Container

### Enter the MySQL Container
To access the MySQL container's shell:

```sh
docker exec -it mysql-container bash
```

### Access the MySQL REPL
To connect to the MySQL database from your host machine:

```sh
mysql -h 127.0.0.1 -P 3306 -u user -puserpassword
```

---

## Accessing phpMyAdmin
Once the containers are running, you can access phpMyAdmin in your browser at:

```
http://localhost:8080
```

Use the following credentials to log in:
- **Server:** `mysql`
- **Username:** `user`
- **Password:** `userpassword`