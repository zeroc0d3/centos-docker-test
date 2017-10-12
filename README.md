# CentOS Docker Test

Docker CentOS Test (Alpha Version), not ready for production.

## Features:
* bash (+ themes)
* oh-my-zsh (+ themes)
* tmux (+ themes)
* vim (+ plugins with vundle & themes)
* rbenv / rvm
  - [X] gem test unit (rspec, serverspec)
  - [X] gem docker-api
  - [X] gem sqlite3, mongoid, sequel, apktools
  - [X] gem mysql2 (run: yum install -y mysql-devel)
  - [X] gem pg, sequel_pg (run: yum install -y postgresql-libs postgresql-devel)
  - [X] gem rubocop
  - [X] [**others**](https://github.com/zeroc0d3/centos-docker-test/blob/master/centos-application/rootfs/root/Gemfile)
* npm
  - [X] npm test unit (ChaiJS, TV4, Newman)
* js package manager
  - [X] yarn
  - [X] bower
  - [X] grunt
  - [X] gulp
  - [X] yeoman
* composer

## Configuration:
* Generate ssh key for your access:
  ```
  ssh-keygen -t rsa
  ```
  or
  ```
  ssh-keygen -t rsa -b 4096 -C "zeroc0d3.team@gmail.com" -f $HOME/.ssh/id_rsa
  ```
* Add your id_rsa.pub to environment (.env) file to run with `docker-compose`, or
* Add your id_rsa.pub to SSH_AUTHORIZED_KEYS in Dockerfile to run with `docker build -t [docker-image-name] [path-dockerfile-folder]`
* Rebuild your docker container
  ```
  docker-compose build && docker-compose up --force-recreate
  ```
* Check your IP Address container
  - Show running container docker
    ```
    docker ps
    ```
  - Show the IP Address container
    ```
    docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' [container_name_or_id]
    ```
    * Read [this](http://stackoverflow.com/questions/17157721/getting-a-docker-containers-ip-address-from-the-host)
  - Inspect container
    ```
    docker inspect [name_container]
    ```
    (eg: application_1)
* Access ssh
  - Run:
    ```
    ssh docker@[ip_address_container]
    ```
  - Superuser access (root):
    ```
    sudo su
    ```
    (password: **docker**)

## Pull:
* git pull --recurse-submodules

## Docker Compose
* Copy `.env.example` to `.env`
* Build & running
  ```
  docker-compose build && docker-compose up
  ```
* Force recreate container
  ```
  docker-compose build && docker-compose up --force-recreate consul ruby postgres application
  ```
* Running container only
  ```
  docker-compose up
  ```

## Environments
You can run docker-compose for different environment with selected containers
* Copy `env.sh.example` to `env.sh`
* Change to execute script
  ```
  chmod a+x env.sh
  ```
* Change environment in `env.sh` file
  ```
  ENV="development"            # (use: "development" or "production" as selected environment)
  CONTAINER_PRODUCTION="..."   # (selected containers will be run in production environment)
  CONTAINER_DEVELOPMENT="..."  # (selected containers will be run in development environment)
  ```
* Running script
  ```
  ./env.sh
  ```

## License
[**GNU General Public License v2**](https://github.com/zeroc0d3/centos-docker-test/blob/master/LICENSE)
