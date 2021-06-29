
# PARTIEL-DOCKER-1469
In this exam, we have to deploy and repair a docker plateform

<br>

## Installation

### Subject

You can download the subject folder of the exam by using this command line :

```bash
bash <(curl -L ​raw.githubusercontent.com/Akasam/samplephpwebsite/master/all_versions.sh)
```

### Work

Download the .tar archive (of the student 1469) which is located in classrooms.

You can untar the rendu folders or navigate in the folders already uncompressed.

Then you just have to navigate in folders <b>rendu_v1/ rendu_v2/ rendu_v3/</b>

<br>

## Usage
You can find at the root of the folder a script :

```bash
./start.sh
```
You can use this by copying this command line in your terminal at the root of your folder.

<br>
This script starts containers and build your docker plateform automatically for you.

<br>

You can also find in the <b>rendu_v*</b> folders nearly the same script.

<br>

## V1

### Brief

This build starts an html page with a php script which helps to navigate through pages.

### What's new

- Adding a docker-compose.yml file
- Creating 2 containers in this file
- Modify config.php => line20: true->false
- Adding a start.sh script

### Explanation

For the docker-compose.yml i added these lines :

```docker
version: "3.3"
services:
    nginx:
        container_name: http
        image: nginx:latest
        volumes:
            - ./_nginx/default.conf:/etc/nginx/conf.d/default.conf
        ports:
            - "8080:80"
        depends_on: 
            - "php"
        
    php:
        container_name: script
        image: php:fpm
        volumes:
            - ./:/var/www/monsite
```

In the config.php file i replaced on line 20 :

```php
'pretty_uri' => false
```

For the start.sh i added these lines :
```bash
#!/bin/bash

docker-compose up -d
read -p "Press any key to continue... " -n1 -s
docker-compose down
```
<br>

## V2

### Brief

This build starts an html page with a php script which helps to navigate through pages.

### What's new

- Templating from v1 for the docker-compose.yml and the change in config.php
- Changing the versions of nginx and php in the docker-compose.yml
- Adding a start.sh script

### Explanation

For the docker-compose.yml i changed these lines :

- Line 5:
```docker
image: nginx:1.12
```
- Line 15:
```docker
image: php:7.1-fpm
```
<br>

The start.sh is the same as the v1

<br>

## V3


### Brief

This build starts an html page with a php script which helps to navigate through pages. There's a built database which is a little bit useless at the moment.

### What's new

- Templating from v2 for the docker-compose.yml and the change in config.php
- Creating a new database container in the docker-compose.yml
- Creating a Dockerfile with php extensions
- Adding a start.sh script

### Explanation

For the docker-compose.yml i added these lines :


- Line 18-19:
```docker
depends_on: 
    - "db"
```

- Line 21 and +:
```docker
db:
        container_name: database
        image: mariadb:10.3
        environment:
            MARIADB_DATABASE: db
            MARIADB_USER: php_user
            MARIADB_PASSWORD: sdrugntqqsciur
            MARIADB_ROOT_PASSWORD: sdrugntqqsciur
```

<br>

The start.sh is the same as the v2
