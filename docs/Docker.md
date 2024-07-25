# Docker

## List downloaded images

```shell
docker images
```

## List running images

```shell
docker ps
```

## List running and stopped images

```shell
docker ps --all 
OR
docker ps -a
```

## Download from dockerHub

```shell
docker pull <imageName>:<TagName>
```

## Run container

```shell
docker run <imageName>:<TagName>
```

## Run the container in the background

```shell
docker run -d redis:7.2-bookworm
```

## Run container in interactive mode

```shell
docker run -it <imagename>:<tagname>
```
