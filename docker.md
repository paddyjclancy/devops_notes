# Docker

###### Learning Docker - https://www.docker.com/101-tutorial
###### PWD = Play With Docker, cloud hosted 


## PWD Activity Notes
A container is simply another process on your machine that has been isolated from all other processes on the host machine.

That isolation leverages kernel namespaces and cgroups, features that have been in Linux for a long time. Docker has worked to make these capabilities approachable and easy to use.

When running a container, it uses an isolated filesystem. This custom filesystem is provided by a **container image**. Since the image contains the container's filesystem, it must contain everything needed to run an application - all dependencies, configuration, scripts, binaries, etc. The image also contains other configuration for the container, such as environment variables, a default command to run, and other metadata.

A **Dockerfile** is simply a text-based script of instructions that is used to create a container image:

```
FROM node:10-alpine						# This image is not stored locally, so will be fetched
WORKDIR /app
COPY . .
RUN yarn install --production			# yarn is an alternative to npm
CMD ["node", "/app/src/index.js"]		# Specifies default command to run when starting container from image
```

- To build an image from the above Dockerfile, enter `$ docker build -t docker-101 .` 
- To start a container and run an application, enter `$ docker run -d -p 3000:3000 docker-101`
		- `-d` - run the container in detached mode (in the background)
		- `-p 80:80` - map port 80 of the host to port 80 in the container

- To see the ID of containers, enter `docker ps`
- To stop a container using its id, enter `docker stop [ID]`
- Remove a halted container using `docker rm [ID]`