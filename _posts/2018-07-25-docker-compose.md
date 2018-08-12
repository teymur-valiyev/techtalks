---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: docker-compose
title: Docker compose
categories: Tutorial
published: false
tags:
- docker
- docker-compose
---

links:

restart: always

volumes

each container restart accure intependetly

many application depends from another service 

depends_on - relationship  - restart will depends on 

## Networking 

default networking bridge

docker network ls


docker network inspect networking_name

docker network create --driver bridge superbridge

docker run -d --name hello --net superbridge tutum/hello-world 

docker network inspect superbridge 
```
networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
  superbridge:
    external: true
```

```
docker-compose port servicename 80
```

share data between containers

## Scale

```
docker-compose scale servicename=2
```


docker-compose exec servername ls

```
docker volume ls 
```

```
volumes_from:
	- servicename:ro
```
ro - read only
get all volumes from another service


```
docker volume create --name images --driver=local
```

external: true - docker-compose add external volume

```
version: '2'
services:
  worker:
    image: tutum/hello-world
    command: sh -c "while true;do echo test; done"
    logging:
      driver: json-file
      options:
        max-file: "5"
        max-size: "1m"
```

docker-compose logs -f

```
docker inspect --format '{{.LogPath}}' containername 
```

configure logging providers

docker-compose up 
pull->build->create->start


docker-compose scale servicename

docker-compose pause servicename
docker-compose unpause servicename

docker-compose port servicename 80 


docker-compose events -  listening for changes

docker-compose config - file gosterir - validate edir compose file

## enviroment variable

.env -file for enviroment
docker-compose reader .env file 

```
version: '2'
services:
  worker:
    image: tutum/hello-world
    env_file:
      - "staging.env"
    ports:
      - 80
```

```
version: '2'
services:
  worker:
    image: tutum/hello-world
    environment:
      - BAR 
    ports:
```

env - shows enviroments 


docker-compose up -f filename.yml


docker-compose.override.yml - docker loads for override

base.yml - docker  

```
version: '2'

services: 
  hello:
    extends:
      file: base.yml
      service: base
    ports:
      - 80
    environment:
      SERVICE: hello
```

docker-compose config