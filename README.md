# Introduction

## Requirements
Requires https://hub.docker.com/ account for storing images non-publicly
Requires the host machine to run docker with docker-compose/docker compose

Source code or node.js program's root folder = the backend folder

Take note of the .dockerignore file which does *not* copy over node_modules on purpose, this is an in-image install step as there is an entirely different OS running in the docker image.

The setup assumes a package.json file is present at the backend root directory for npm install

The setup assumes a genfanad account exists at dockerhub with the repositories that follow each image's name in the yml files such as:
genfanad/backend

This might be the only image required, unless you already run more than 1 process per world, the MariaDB image, or any currently used SQL DB equivalent also exists and would configure roughly the same, this just serves as an example of that.

## Building
Builds and pushes the current backend (assumes that there is a package.json file at the very root of backend folder, and that there is a server.js:
docker-compose -f docker-compose-build.yml build
docker-compose -f docker-compose-build.yml push

## Running

ctrl+c will help with exiting from tools such as `docker stats`

### If using 1 db for all worlds:
`docker-compose -f docker-compose-example-2-worlds-1-db.yml up -d`

To get a brief overview of what's running after that:
`docker stats`

Check logs to see if anything errored:

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs backend-w1`

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs backend-w2`

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs mysql`


### If using 1 db per world:
`docker-compose -f docker-compose-example-2-worlds-2-db.yml up -d`

To get a brief overview of what's running after that:
`docker stats`

Check logs to see if anything errored:

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs backend-w1`

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs backend-w2`

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs mysql-w1`

`docker-compose -f docker-compose-example-2-worlds-2-db.yml logs mysql-w2`


