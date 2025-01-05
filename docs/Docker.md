# Docker

## List downloaded images

```shell
docker images
OR
docker image ls
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

`run` verifies if the image is already available locally. If not, it downloads the image, if available on the docker hub and then runs it.

```shell
docker run <imageName>:<TagName>
```

## Run the container in the background

`d` refers to detached mode.

```shell
docker run -d redis:7.2-bookworm
```

## Run container in interactive mode

```shell
docker run -it <imagename>:<tagname>
```

## Stop a running container

```shell
docker stop <container name>
```

## Port binding example

Run nginx server and use the port binding to see the page on the `localhost`

```shell
docker run nginx

>> Unable to find image 'nginx:latest' locally
>> latest: Pulling from library/nginx
```

The above command doesnt do much, as the port binding is not done to see the default page in the browser.

```shell
docker run -p 80:80 nginx

>> Unable to find image 'nginx:latest' locally
>> latest: Pulling from library/nginx
```

![](C:\Users\jeeva\AppData\Roaming\marktext\images\2024-08-04-09-45-13-image.png)

To bind the port to port number `5000` in your system

```shell
docker run -p 5000:80 nginx

>> Unable to find image 'nginx:latest' locally
>> latest: Pulling from library/nginx
```

![](C:\Users\jeeva\AppData\Roaming\marktext\images\2024-08-04-09-46-29-image.png)

## Delete all the stopped containers

Stopped containers accumulate unless you delete it. It can be deleted from the docker desktop or using below command.

```shell
docker container prune
```

### Automatically delete the container after it stops

Use `--rm` flag to the `run` command to automatically delete the container after it is stopped.

```shell
docker run -p 5000:80 nginx --rm -d

>> Unable to find image 'nginx:latest' locally
>> latest: Pulling from library/nginx
```

## Environment variables

To pass environment variables at run time

```shell
docker run -e JIRA_PAT=MYuOUgiy22435FHTFyt87108cywiu9
```

## Slim and alpine images

`Slim` images are lower in size compared to the original image. `Alpine` images are still more smaller in size compared to slim. `Slim` images are mostly based on the debian distro whereas `Alpine` images are based on `Arch` linux. 

## Run a command in a running container

To run a command or open the bash in  an already running container;

```shell
docker exec -it objective_poincare /bin/bash
```

This opens a shell in the container in the already running container `objective_poincare`

## Build a a custom docker image

To build a custom docker image you need a `Dockerfile` 

```dockerfile
# Dockerfile


FROM debian:bookworm-slim
RUN apt update
RUN apt install -y python3 python3-pip git
WORKDIR /app
RUN git clone https://github.com/deluge-torrent/deluge.git
WORKDIR /app/deluge
CMD [ "bash" ]
```

This command is used to build a `Dockerfile` to an image. `.` represent the path where docker has to look to find the `Dockerfile` , current directory in this case.

```shell
docker build -t debian:1.0.0 .

OR

docker build -t debian:1.0.0 -f <path to Dockerfile>
```
