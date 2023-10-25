# Traefik Gateway for Docker Services (Docker Compose)

This repository provides a Traefik gateway configuration for managing Docker services using Docker Compose.

## Flavors

Choose from the following flavors:

- **ingress**: Standard configuration for exposing Docker containers.
- **ingress-vpn**: A configuration for use with VPN connections (generic).

## Getting Started with Ingress Flavor

### Setup

To get started with the **ingress** flavor, run the following command:

```shell
ingress/setup-docker-env
```

This command will create an "ingress" network for exposing Docker containers and an ACME volume for storing SSL/TLS certificates.

### Entrypoints

  - http
  - https

### ACME Resolvers (Let's Encrypt)

  - http

### Middlewares

  - http2https@file - redirection from http:// to https://

### Exposing services

```
    ...
  services:
    example:
      image: ...
      labels:
        - expose.ingress=yes
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-http.rule=Host(`sample.example.com`)
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-https.rule=Host(`sample.example.com`)
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-http.entrypoints=http
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-https.entrypoints=https
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-https.tls.certresolver=http
        - traefik.http.routers.${COMPOSE_PROJECT_NAME}-http.middlewares=http2https@file
      networks:
        default:
          priority: 500
        ingress:
          priority: 100

  networks:
    ingress:
      external: true
      name: ingress
```
