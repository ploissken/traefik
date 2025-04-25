```shell

████████╗██████╗  █████╗ ███████╗███████╗██╗██╗  ██╗
╚══██╔══╝██╔══██╗██╔══██╗██╔════╝██╔════╝██║██║ ██╔╝
   ██║   ██████╔╝███████║█████╗  █████╗  ██║█████╔╝
   ██║   ██╔══██╗██╔══██║██╔══╝  ██╔══╝  ██║██╔═██╗
   ██║   ██║  ██║██║  ██║███████╗██║     ██║██║  ██╗
   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝

       A docker container to serve them all.


```

## You will need [Docker](https://docker.com) (v28 or later) and Docker Compose (v2.30 or later).

This is [Traefik](https://traefik.io/) encapsulated into a docker container, for serving multiple docker containers into a single server with out-of-the-box SSL using Lets Encrypt and subdomain handling. Pretty noice. Based on [traefik-best-practice](https://github.com/bluepuma77/traefik-best-practice/tree/main/docker-traefik-dashboard-letsencrypt).

## Config

You need a .env file containing two secrets in order to boot this container.
The email is necessary to sign your SSL; Dashboard host is the browser url for traefik dashboard's in your host.

```

EMAIL=email@sample.com
DASHBOARD_HOST=dashboard.sample.com

```

---

## Sample container orchaestration

This is a sample docker-compose.yml to run a node project thru npm.

Requires a .env with:

```
PORT=3000
SERVICE_URL=your.domain.com

```

```
services:
  YOUR_SERVICE_NAME:
    image: node:23-slim
    container_name: YOUR_SERVICE_NAME
    restart: unless-stopped
    working_dir: /home/node
    volumes:
      - ./:/home/node/:cached
    command: bash -c "npm install && npm run start"
    environment:
      - HOST=0.0.0.0
      - PORT=${PORT}
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.YOUR_SERVICE_NAME.rule=Host(`${SERVICE_URL}`)"
      - "traefik.http.routers.YOUR_SERVICE_NAME.entrypoints=websecure"
      - "traefik.http.routers.YOUR_SERVICE_NAME.tls.certresolver=myresolver"
      - "traefik.http.services.YOUR_SERVICE_NAME.loadbalancer.server.port=${PORT}"
    networks:
      - traefik

networks:
  traefik:
    external: true


```

---

## Starting in production environment

```

docker compose up

```
