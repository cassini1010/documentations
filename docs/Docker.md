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

## Run image

```shell
docker run <imageName>:<TagName>
```

## Run the image in the background

```shell
docker run -d redis:7.2-bookworm
```

## Run image in interactive mode

```shell
docker run -it <imagename>:<tagname>
```
