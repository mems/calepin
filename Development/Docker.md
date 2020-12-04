## How to use docker

- [Tobias T– | Docker](https://tobiastom.name/explains/docker)
- [Building Efficient Dockerfiles - Node.js - bitJudo](http://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/)
- [Kubernetes: An Introduction to Deploying a Node.js Docker App — SitePoint](https://www.sitepoint.com/kubernetes-deploy-node-js-docker-app/)
- [Running java on Docker images on your Mac – A getting started guide | Jeroen van Wilgenburg](https://vanwilgenburg.wordpress.com/2017/05/15/running-java-on-docker-images-on-your-mac-a-getting-started-guide/)
- [Tutoriel pour apprendre à utilisation Docker](https://xataz.developpez.com/tutoriels/utilisation-docker/)
- [docker-basicLearning/README.md at master · championshuttler/docker-basicLearning](https://github.com/championshuttler/docker-basicLearning/blob/master/README.md)
- [How to Use a Remote Docker Server to Speed Up Your Workflow | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-a-remote-docker-server-to-speed-up-your-workflow)

## Alpine

```dockerfile
FROM alpine:3.11

RUN set -x \
    && apk add --no-cache bash
```

- [Alpine Linux packages](https://pkgs.alpinelinux.org/packages?name=npm&branch=edge#)
- [Alpine Linux package management - Alpine Linux](https://wiki.alpinelinux.org/wiki/Alpine_Linux_package_management)

```sh
apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main package
```

http://nl.alpinelinux.org/alpine/v3.11/main/
http://dl-cdn.alpinelinux.org/alpine/edge/community

- [Official Alpine Linux mirrors](https://mirrors.alpinelinux.org/)
- [Template:Mirrors - Alpine Linux](https://wiki.alpinelinux.org/wiki/Template:Mirrors)
- https://gitlab.alpinelinux.org/alpine/aports/-/blob/master/main/alpine-mirrors/mirrors.yaml

## How docker works

- [How Docker Works - Intro to Namespaces - YouTube](https://www.youtube.com/watch?v=-YnMr1lj4Z8)
- [Introduction to Docker for CTFs - YouTube](https://www.youtube.com/watch?v=cPGZMt4cJ0I)

## AMP

Aka LAMP, Linux Apache MySQL PHP

- [PHP, Apache, MySQL within Docker containers | Cloudreach](https://www.cloudreach.com/en/resources/blog/ct-apache-docker-containers/)
- [docker-compose with php/mysql/phpmyadmin/apache](https://gist.github.com/jcavat/2ed51c6371b9b488d6a940ba1049189b)
- [nystudio107 | An Annotated Docker Config for Frontend Web Development](https://nystudio107.com/blog/an-annotated-docker-config-for-frontend-web-development)

## Optimizations

- [Optimizing Dockerfile for Node.js (Part 1) - js.io](https://web.archive.org/web/20200913150039/https://js.io/optimizing-dockerfile-for-node-js-part-1)

## Virtual Machine

If the host is not linux or the image use on other OS use a virtual machine container

- [docker - Can Windows Containers be hosted on linux? - Stack Overflow](https://stackoverflow.com/questions/42158596/can-windows-containers-be-hosted-on-linux)
- [Running Docker on Apple Silicon M1 (follow-up) — finestructure](https://web.archive.org/web/20201127230755/https://finestructure.co/blog/2020/11/27/running-docker-on-apple-silicon-m1-follow-up) and [Running Docker on Apple Silicon M1 — finestructure](https://web.archive.org/web/20201128004304/https://finestructure.co/blog/2020/11/27/running-docker-on-apple-silicon-m1)
- [hectorm/docker-qemu-reactos: A Docker image for the ReactOS operating system.](https://github.com/hectorm/docker-qemu-reactos) or [Héctor Molinero Fernández / docker-qemu-reactos · GitLab](https://gitlab.com/hectorm/docker-qemu-reactos) - [VirtualBox - ReactOS Wiki](https://reactos.org/wiki/VirtualBox)
