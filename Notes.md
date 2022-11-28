## Some Docker commands

```docker
# Delete all unused images

$ docker image prune -a


# Specify port

# exposed-port:docker-internal-port

$ docker run -p 3000:4000 image-name


# Removing container automatically when stop

$ docker run --rm image-name


# Building an image with name

# image-name = goals
# version/tag = latest
# docker file path = .

$ docker build -t goals:latest .


# Naming container

# container-name = goalsapp (--name)
# image-name = goals
# version/tag = latest
# exposed-port = 3000 (-p)
# internal-container-port = 4000 (-p)
# detached = true (-d)
# remove when stop = true (--rm)

$ docker run -p 3000:4000 -d --rm --name goalsapp goals:latest




```
