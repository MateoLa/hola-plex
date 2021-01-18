# Hola-Plex

Trying to secure Hola-Plex:

## Prerequisites

You need to have docker and docker-compose installed in your host machine.

## Instructions to reproduce:

1) cd into any folder to clone the repo:
```bash
git clone https://github.com/MateoLa/hola-plex.git
```

2) cd into hola-plex and run:
```bash
docker-compose up --build
```
With "docker ps" you will see 2 containers started: nginx and plex.
Navigate to: localhost.
You'll be redirected to localhost/web/inxex.html where you can reproduce any movie from the list.

Navigate to: https://localhost.
You won't be connect to the secured page.

3) From another console run:
```bash
docker run --name nginx_new --rm -v /absolute-path-to/hola-plex/nginx:/etc/nginx/conf.d -p 443:443 --network hola-plex_hola-net nginx:alpine
```
(In my case the command is: "docker run --name nginx_new --rm -v /home/mateo/epa/hola-plex/nginx:/etc/nginx/conf.d -p 443:443 --network hola-plex_hola-net nginx:alpine")
With "docker ps" you will see a third container running: nginx_new.
Navigate to: https://localhost.
Now you will see your "self" secured page.

## Why the nginx_new container is upstream capable and the nginx container don't?

