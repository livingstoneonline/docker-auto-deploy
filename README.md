# Docker Auto Deploy

[![Docker Stars](https://img.shields.io/docker/stars/livingstone/auto-deploy.svg)][hub]
[![Docker Pulls](https://img.shields.io/docker/pulls/livingstone/auto-deploy.svg)][hub]
[![Image Size](https://img.shields.io/imagelayers/image-size/livingstone/auto-deploy/latest.svg)](https://imagelayers.io/?images=livingstone/auto-deploy:latest)
[![Image Layers](https://img.shields.io/imagelayers/layers/livingstone/auto-deploy/latest.svg)](https://imagelayers.io/?images=livingstone/auto-deploy:latest)

### Introduction

Super simple listener base based on
[docker-hook](https://github.com/schickling/docker-hook).

Used to trigger re-deployment when any Docker Hub web-hook is fired.

### Includes

* [Alpine Linux](http://alpinelinux.org/)
* python 2.7
* docker
* docker-compose

### Notes

Here is an example **docker-compose.yml** file that uses this Docker Image, to
listen to web-hooks on port **8080**. When a hook is received, it will trigger
```docker-compose pull``` and ```docker-compose up -d``` in the volume
__/deploy__.

```yml
version: "2"
services:
  auto-deploy: 
    build: ./
    image: "livingstone/auto-deploy"
    container_name: docker-auto-deploy
    restart: always
    environment:
      - "DIR=/opt/docker-image"
      - "AUTH_TOKEN=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "/root/.docker:/root/.docker"
      - "/opt/docker-image:/opt/docker-image"
    ports:
      - "8000:8000"
```

### Current maintainers

* [Nigel Banks](https://github.com/livingstone)
