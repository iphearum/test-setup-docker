# Installation
+ To get started, the following steps needs to be taken:
+ Clone the repo.
+ `cd laravel-docker-postgres` to the project directory.
+ `cd` to web and run the command to create a new Laravel project into **application** directory.
+ `cd ..` to back the project directory.
+ `cp .env.example .env` to use env config file
+ Run `docker-compose up -d` to start the containers.
+ Visit http://localhost to see your Laravel application.
+ Try to connect 127.0.0.1:5432 to access Postgres
+ After starting, note that one directory and one file will be created with name *postgres* and file *data*, this files are Database archives

# Env config
+ [env] file is to config name/path


# usage:
+ `docker-compose up -d` to start all containers
+ `docker-compose down` to stop all containers
+ If you need to restart after modifying *docker-compose.yml* restart with `docker-compose down` and `docker-compose up -d`

# Images
+ redis:alpine
+ postgres:9.5-alpine
+ nginx:alpine
+ php8-fpm:latest

# SourceFiles

## Into **sourcefiles** directory, exists others directories: **php-fpm** and **nginx**:


### php-fpm: Extensions PHP and PHP.INI
+ Dockerfile: php8.1-pgsql php8.1-gd php-redis
+ php-ini-overrides.ini

### nginx: nginx.conf
+ file conf nginx

### volumes:
- nginx folder
- php-ini-overrides.ini
- data(postgres)

### multiple servers:
- create file conf of nginx in nginx directory you should use default.conf as exemple
- restart containers: `docker-compose down` and `docker-composer up -d`


# Troubleshooting

## If you need to restart after modifying *Dockerfile* and have Troubleshooting:
+ [remove] Stop all containers running `docker kill $(docker ps -q)`
+ Remove all containers running `docker rmi $(docker images -q)`
+ Verify all containers running: `docker ps -a`
+ Stop all containers and remove: `docker stop $(docker ps -a -q)` and `docker rm $(docker ps -a -q)`
+ Try to start again `docker-compose up -d`
+ Try to reinstall `docker-compose up -d --remove-orphans` with `--remove-orphans` option
+ Remove all volumes from docker `docker system prune --all --volumes`
+ Remove and reinstall `docker kill $(docker ps -q) && docker rm $(docker ps -a -q) && docker rmi $(docker images -q) && docker-compose build && docker-compose up -d --remove-orphans`

# Force remove containers docker
+ restart docker `sudo systemctl restart docker.socket docker.service`
+ remove constaints id `docker rm $(docker ps -a -q)`

# Remove volumes from docker
+ Remove valumes `docker system prune`
+ Remove all volumes from docker `docker system prune --all` or `docker system prune -a`
+ Remove all image valumes `docker image prune`