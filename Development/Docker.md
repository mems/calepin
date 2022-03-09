## How to use docker

- [Tobias T– | Docker](https://tobiastom.name/explains/docker)
- [Building Efficient Dockerfiles - Node.js - bitJudo](http://bitjudo.com/blog/2014/03/13/building-efficient-dockerfiles-node-dot-js/)
- [Kubernetes: An Introduction to Deploying a Node.js Docker App — SitePoint](https://www.sitepoint.com/kubernetes-deploy-node-js-docker-app/)
- [Running java on Docker images on your Mac – A getting started guide | Jeroen van Wilgenburg](https://vanwilgenburg.wordpress.com/2017/05/15/running-java-on-docker-images-on-your-mac-a-getting-started-guide/)
- [Tutoriel pour apprendre à utilisation Docker](https://xataz.developpez.com/tutoriels/utilisation-docker/)
- [docker-basicLearning/README.md at master · championshuttler/docker-basicLearning](https://github.com/championshuttler/docker-basicLearning/blob/master/README.md)
- [How to Use a Remote Docker Server to Speed Up Your Workflow | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-a-remote-docker-server-to-speed-up-your-workflow)

## Best-practices

Aka optimizations

- [hexops/dockerfile: Dockerfile best-practices for writing production-worthy Docker images.](https://github.com/hexops/dockerfile)
- [Best practices for writing Dockerfiles | Docker Documentation](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [aquasecurity/trivy: A Simple and Comprehensive Vulnerability Scanner for Containers, Suitable for CI](https://github.com/aquasecurity/trivy)
- [Optimizing Dockerfile for Node.js (Part 1) - js.io](https://web.archive.org/web/20200913150039/https://js.io/optimizing-dockerfile-for-node-js-part-1)
- [Optimizing Docker image size and why it matters - contains.dev](https://web.archive.org/web/20220109024111/https://contains.dev/blog/optimizing-docker-image-size)
- [Optimizing Docker image size and why it matters | Hacker News](https://news.ycombinator.com/item?id=29828386)
- [Docker optimization guide: the 5 best tips to optimize Docker development speed](https://web.archive.org/web/20220227213557/https://www.augmentedmind.de/2022/01/09/optimize-docker-development-speed/)
- [Docker optimization guide: optimize build speed in CI pipelines](https://web.archive.org/web/20220220192205/https://www.augmentedmind.de/2022/01/23/optimize-docker-build-speed-in-ci/)
- [Docker optimization guide: 8 tricks to optimize your Docker image size](https://web.archive.org/web/20220220191209/https://www.augmentedmind.de/2022/02/06/optimize-docker-image-size/)
- [Docker optimization guide: the 12 best tips to optimize Docker image security](https://web.archive.org/web/20220220192213/https://www.augmentedmind.de/2022/02/20/optimize-docker-image-security/)

> Perform your add & remove operations in the same RUN command. Doing them separately creates two separate layers which inflates the image size.
>
> This creates two image layers - the first layer has all the added foo, including any intermediate artifacts. Then the second layer removes the intermediate artifacts, but that's saved as a diff against the previous layer:
>
> ```docker
RUN ./install-foo
RUN ./cleanup-foo
```
>
> Instead, you need to do them in the same RUN command:
>
> ```docker
RUN ./insall-foo && ./cleanup-foo
```
>
> This creates a single layer which has only the foo artifacts you need.
>
> This why the [official Dockerfile best practices show](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#run) the apt cache being cleaned up in the same RUN command:
>
> ```docker
RUN apt-get update && apt-get install -y \
	package-bar \
	package-baz \
	package-foo  \
	&& rm -rf /var/lib/apt/lists/*
```
>
> — [A common mistake that's not covered in this article is the need to perform your ... | Hacker News](https://news.ycombinator.com/item?id=29830364)

```docker
RUN <<EOF
	apt-get update
	apt-get install -y foo bar baz
	etc...
EOF
```

Lint and security:

- [Docker Security Best Practices from the Dockerfile](https://web.archive.org/web/20210104021357/https://cloudberry.engineering/article/dockerfile-security-best-practices/)
- [goodwithtech/dockle: Container Image Linter for Security, Helping build the Best-Practice Docker Image, Easy to start](https://github.com/goodwithtech/dockle)
- [hadolint/hadolint: Dockerfile linter, validate inline bash, written in Haskell](https://github.com/hadolint/hadolint)

## Docker compose

Aka `compose.yaml` (or `docker-compose.yml` or `compose.yml`)

- [YAML is a superset of JSON](../Formats%2C%20encoding%20and%20protocols/YAML/YAML.md#yaml-is-a-superset-of-json)
- [bucherfa/docker-compose-converter: Convert docker run/create commands to docker-compose.yml files.](https://github.com/bucherfa/docker-compose-converter)
- [Compose file | Docker Documentation](https://docs.docker.com/compose/compose-file/)

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

## Virtual Machine

If the host is not Linux or the image use on other OS use a virtual machine container

- [docker - Can Windows Containers be hosted on linux? - Stack Overflow](https://stackoverflow.com/questions/42158596/can-windows-containers-be-hosted-on-linux)
- [Running Docker on Apple Silicon M1 (follow-up) — finestructure](https://web.archive.org/web/20201127230755/https://finestructure.co/blog/2020/11/27/running-docker-on-apple-silicon-m1-follow-up) and [Running Docker on Apple Silicon M1 — finestructure](https://web.archive.org/web/20201128004304/https://finestructure.co/blog/2020/11/27/running-docker-on-apple-silicon-m1)
- [hectorm/docker-qemu-reactos: A Docker image for the ReactOS operating system.](https://github.com/hectorm/docker-qemu-reactos) or [Héctor Molinero Fernández / docker-qemu-reactos · GitLab](https://gitlab.com/hectorm/docker-qemu-reactos) - [VirtualBox - ReactOS Wiki](https://reactos.org/wiki/VirtualBox)

### macOS

- [sickcodes/docker-osx - Docker Image | Docker Hub](https://hub.docker.com/r/sickcodes/docker-osx) - [sickcodes/Docker-OSX: Run Mac in a Docker! Run near native OSX-KVM in Docker! X11 Forwarding! CI/CD for OS X!](https://github.com/sickcodes/Docker-OSX)
- [Install on Virtual Machine](../Operating%20Systems/macOS/macOS.md#install-on-virtual-machine)

## Volumes

- [How to list the content of a named volume in docker 1.9+? - Stack Overflow](https://stackoverflow.com/questions/34803466/how-to-list-the-content-of-a-named-volume-in-docker-1-9)
