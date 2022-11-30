## Some Docker commands

## Images

### Delete all unused images

```docker shell
$ docker image prune -a
```

### Specify port

- exposed-port:docker-internal-port

```docker shell
$ docker run -p 3000:4000 image-name
```

### Removing container automatically when stop

```docker shell
$ docker run --rm image-name
```

### Building an image with name

- image-name = goals
- version/tag = latest
- docker file path = .

```docker shell
$ docker build -t goals:latest .
```

## Containers

### Naming container

- container-name = goalsapp (--name)
- image-name = goals
- version/tag = latest
- exposed-port = 3000 (-p)
- internal-container-port = 4000 (-p)
- detached = true (-d)
- remove when stop = true (--rm)

```docker shell
$ docker run -p 3000:4000 -d --rm --name goalsapp goals:latest
```

### Volumes

> Notes: We have a problem with this structure. All of files are being replaced by local files with volume 2

> To solve it, we can add an extra anonymous volume to don't replace the node_modules path. Ex: "-v /app/node_modules"

- volume 1

  - name: feedback
  - path in docker container: /app/feedback

- volume 2
  - name: undefined
  - path local: "/home/vitor/projects/private/docker-course/data-volumes-01-starting-setup:/app"
  - path in docker container: /app

```docker shell
$ docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/home/vitor/projects/private/docker-course/data-volumes-01-starting-setup:/app" feedback-node:volumes
```

#### Fixed command

```docker shell
$ docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback -v "/home/vitor/projects/private/docker-course/data-volumes-01-starting-setup:/app" -v /app/node_modules feedback-node:volumes
```

#### Overview

Ways to create volumes

##### Anonymous Volume

```docker shell
$ docker run -v /app/data
```

##### Named Volume

```docker shell
$ docker run -v data:/app/data
```

##### Bind Mount

```docker shell
$ docker run -v /path/to/code:/app/code

# to read only, add an extra :ro after internal path container

$ docker run -v /path/to/code:/app/code:ro
```
