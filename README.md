```shell

████████╗██████╗  █████╗ ███████╗███████╗██╗██╗  ██╗
╚══██╔══╝██╔══██╗██╔══██╗██╔════╝██╔════╝██║██║ ██╔╝
   ██║   ██████╔╝███████║█████╗  █████╗  ██║█████╔╝ 
   ██║   ██╔══██╗██╔══██║██╔══╝  ██╔══╝  ██║██╔═██╗ 
   ██║   ██║  ██║██║  ██║███████╗██║     ██║██║  ██╗
   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝     ╚═╝╚═╝  ╚═╝

       A docker container to serve them all.


```

You will need [Docker](https://docker.com) (v18.03 or later) and Docker Compose (v1.21.1 or later).
---

This is [Traefik](https://traefik.io/) encapsulated into a docker container, for serving multiple docker containers
into a single server with out-of-the-box SSL and subdomain handling.


## Starting in development environment

docker-compose.yml contains default container information.
The .override contains development variables for local environment. To build and run the container:

```
docker-compose up -d
```

As the container goes up, you will be able to access the [traefik monitoring menu](http://traefik.localhost).

---

## Starting in production environment

The docker-compose.prod.yml contains the overriding information for the production
environment. It must be explicitly called with: 

```

docker-compose -f docker-compose.yml -f docker-compose.prod.yml up

```

As the container goes up, you will be able to access the [traefik monitoring menu](https://traefik.mercuryou.com).
