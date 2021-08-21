# Docker-Compose 

Using Compose is basically a three-step process:

1. Define your app’s environment with a Dockerfile so it can be reproduced anywhere.

2. Define the services that make up your app in docker-compose.yml so they can be run together in an isolated environment.

3. Run `docker compose up` and the Docker compose command starts and runs your entire app. Run `docker compose build` to update any changes to the docker compse file. 


Lets define all services in a config file, that can spin up all the containers that we need 

1. Make a file called `docker-compose.yml`

```YAML
# Version of the compose file format 
version: "3.9"
# Container services
services:
  db:
  #  # image to fetch from docker hub
    image: mongo
    # Mapping of container port to host
    ports:
      - "27017:27017"
      # Mount volume 
    volumes:
      - "db:/data/db"

  app:
  # Path to Dockerfile 
    build: ./app
    restart: always
    ports:
      - "3000:3000"
    # Environment variables for startup script
    # container will use these variables
    # to start the container with these define variables. 
    environment:
      - DB_HOST=mongodb://db:27017/posts
    depends_on:
      - db
    # links:
    #     - ""
```

2. Run `docker compose up` 