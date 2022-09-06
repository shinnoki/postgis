
# postgis

Providing `postgis` image for linux/amd64 and linux/arm64, based on the code copied from [`postgis/docker-postgis`](https://github.com/postgis/docker-postgis).

## Motivation

[Official `postgis/postgis` image](https://registry.hub.docker.com/r/postgis/postgis) only provides image for linux/amd64, so when using postgis, `docker compose up --build` on linux/arm64 fails. Postgis does not provide linux/arm64 image until now, even though the issue reported in Dec. 2020.  
Copying `Dockerfile` and building image locally will solve this issue, but every new release of postgis will delete previous version and fails `RUN apt-get update` in Dockerfile.  
Creating and publishing a Docker image using Github packages allows us to handle this and provide a fixed-version postgis package.  

## Versions used in this image

Postgres 13-bullseye  
Postgis 3.2.3  

## LICENSES

Source code of this image was taken from [`postgis/docker-postgis`](https://github.com/postgis/docker-postgis), Copyright 2014 Original Authors. This package is licensed under the MIT license. See [docker-postgis/LICENSE](https://github.com/postgis/docker-postgis/blob/master/LICENSE) for details.

## How to use

After following the [Quickstart with Docker](https://hasura.io/docs/latest/getting-started/docker-simple/) guide, add `postgis` to services like below.

```yaml:docker-compose.yml
version: '3.7'
services:
  postgres:
    image: ghcr.io/wasd-inc/postgis
    environment:
      POSTGRES_USER: ...
      POSTGRES_PASSWORD: ...
      POSTGRES_DB: ...
    volumes:
      - db-data:/var/lib/postgresql/data
    ports:
      - 5432:5432
    healthcheck: ...
volumes:
  db_data:
```
