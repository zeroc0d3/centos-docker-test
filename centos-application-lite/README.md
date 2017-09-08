# CentOS Application Lite Edition Docker (Application-Lite Container)
[![Build Status](https://travis-ci.org/zeroc0d3lab/centos-application-lite.svg?branch=master)](https://travis-ci.org/zeroc0d3lab/centos-application-lite) [![](https://images.microbadger.com/badges/image/zeroc0d3lab/centos-application-lite:latest.svg)](https://microbadger.com/images/zeroc0d3lab/centos-application-lite:latest "Layers") [![](https://images.microbadger.com/badges/version/zeroc0d3lab/centos-application-lite:latest.svg)](https://microbadger.com/images/zeroc0d3lab/centos-application-lite:latest "Version") [![GitHub issues](https://img.shields.io/github/issues/zeroc0d3lab/centos-application-lite.svg)](https://github.com/zeroc0d3lab/centos-application-lite/issues) [![GitHub forks](https://img.shields.io/github/forks/zeroc0d3lab/centos-application-lite.svg)](https://github.com/zeroc0d3lab/centos-application-lite/network) [![GitHub stars](https://img.shields.io/github/stars/zeroc0d3lab/centos-application-lite.svg)](https://github.com/zeroc0d3lab/centos-application-lite/stargazers) [![GitHub license](https://img.shields.io/badge/license-GPLv2-blue.svg)](https://raw.githubusercontent.com/zeroc0d3lab/centos-application-lite/master/LICENSE.GPL)

This docker image includes:

## Features:
* bash (+ themes)
* oh-my-zsh (+ themes)
* tmux (+ themes)

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
    (eg: application-lite_1)
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

## License
GNU General Public License v2
