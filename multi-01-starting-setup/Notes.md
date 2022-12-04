# Commands

## Network

### Create network

```docker shell
$ docker network create goals-net
```

## MongoDB

### Run MongoDB Container

```docker shell
$ docker run --name mongodb -e MONGO_INITDB_ROOT_USERNAME=vitor -e MONGO_INITDB_ROOT_PASSWORD=secret -v data:/data/db --rm -d --network goals-net mongo
```

## Backend

#### Build Node API Image

```docker shell
$ docker build -t goals-node .
```

#### Run Node API Container

```docker shell
$ docker run --name goals-backend -e MONGODB_USERNAME=vitor -e MONGODB_PASSWORD=secret -v logs:/app/logs -v /home/vitor/projects/private/docker-course/multi-01-starting-setup/backend:/app -v /app/node_modules --rm -d --network goals-net -p 80:80 goals-node
```

## Frontend

#### Build React Image

```docker shell
$ docker build -t goals-react .
```

#### Run React Container

```docker shell
$ docker run --name goals-frontend -v /home/vitor/projects/private/docker-course/multi-01-starting-setup/frontend/src:/app/src --rm -d -p 3000:3000 -it goals-react
```

## Stop containers

```docker shell
$ docker stop goals-frontend goals-backend mongodb
```
