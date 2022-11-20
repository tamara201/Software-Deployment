# Lab3

The task for Lab3 is to create two docker containers, one that contains Wordpress and one that contains a MySQL database. This task consist of 2 parts:
- Part 1: Create a docker-compose file that uses a Wordpress and MySQL image to set up a Wordpress container infrastructure
- Part 2: Create your own images based on debian for a Wordpress container installation

## Part 1

The docker-compose file was created following those two tutorials [Quickstart: Compose and WordPress](https://github.com/docker/awesome-compose/tree/master/official-documentation-samples/wordpress) and [Wordpress & Docker](https://gist.github.com/bradtraversy/faa8de544c62eef3f31de406982f1d42) with few adaptations. 
In order to run the container, following command needs to be executed in the Teil1 folder:

    docker-compose up -d

When entering http://localhost:8080 in the browser you can see the language selection page of Wordpress.
Afterwards, stop the containers or remove them with the following command to avoid conflicts with part 2.

    docker-compose down -v

## Part 2

Several tutorials were used for this part, including those of the lecturer:
- [How To Install Linux, Apache, MySQL, PHP (LAMP) stack on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04)
- [How To Install WordPress with LAMP on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-with-lamp-on-ubuntu-16-04)

In order to build the Wordpress and MySQL images, navigate to the folders where the respective dockerfile is inside and execute the following command:

    docker build -t dockerfile .
    
To create the containers, navigate to the folder Teil2 where the docker-compose file is and execute the command below.

    docker-compose up -d
    
> **_NOTE:_**  It is not necessary to build the images seperately since calling `docker-compose up -d` the images will be build automatically during the execution.

When entering http://localhost:8080/wordpress in the browser you can see the language selection page of Wordpress.
Afterwards, you can stop the containers or remove them with the following command:

    docker-compose down -v
    
## Personal experience

With the first part of this task I had no issues. 
However, during the second part I had problems with the MySQL and Wordpress images. 
I was able to build them, but the containers kept restarting. 
After changing `RUN` to `CMD` in the code below in the MySQL dockerfile and adding `CMD apachectl -D FOREGROUND` to the Wordpress dockerfile, the containers worked properly.

```
CMD service mysql restart && \
     mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "CREATE DATABASE IF NOT EXISTS $MYSQL_DATABASE;" && \
     mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "CREATE USER '$MYSQL_USER'@'%' IDENTIFIED BY '$MYSQL_PASSWORD';" || true && \
     mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "SET PASSWORD FOR $MYSQL_USER=PASSWORD('$MYSQL_PASSWORD');" && \
     mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "GRANT ALL PRIVILEGES ON $MYSQL_DATABASE.* TO '$MYSQL_USER'@'%';" && \
     mysql --user=root --password=$MYSQL_ROOT_PASSWORD -e "FLUSH PRIVILEGES;" && \
     mysqld
```
     
