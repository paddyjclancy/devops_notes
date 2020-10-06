# Containerisation

A _Dockerfile_ is simply a text-based script of instructions that is used to create a container image from code:

```
FROM node:10-alpine				  	# This image is not stored locally, so will be fetched
WORKDIR /app
COPY . .
RUN yarn install --production			# yarn is an alternative to npm
CMD ["node", "/app/src/index.js"]		# Specifies default command to run when starting container from image
```

- "INSTRUCTION" "value"
- Instructions are capitalised
- FROM is always first, and shows the base image
- Some instructions add image layers, others only metadata
- To build an image from the above Dockerfile, enter `$ docker build -t docker-101 .`
	- **Run this in the directory containing the Dockerfile**
- To start a container and run an application, enter `$ docker run -d -p 3000:3000 docker-101`
	- `-d` - run the container in detached mode (in the background)
	- `-p 80:80` - map port 80 of the host to port 80 in the container
- To see the ID of containers, enter `docker ps`
- To enter into a container, and do something with it, use `docker exec [ID]` `cat /data.txt`
- To stop a container using its id, enter `docker stop [ID]`
- Remove a halted container using `docker rm [ID]`

### Multi-stage Builds

For when starting image is too large / monolithic - breaks it down into multiple sections.

Multiple `FROM` sections within a single Dockerfile which mark different steps

Final section tends to include multiple `COPY FROM` commands, which combine all previous outputted images into this one.

### Working with Containers
When using containers, the image stays the same and a new layer specific to the container is added.

Stopping or pausing does not get rid of a container, it _must_ be deleted - this is __persistance__.

The container does not include kernels - it shares that of its host machine.
  - Windows host = Windows contaienr
  - Linux = Linux

Each container should generally contain just a single service, in keeping with the __Separation of Concerns__ practice.

### Logging

Logs found in either _systemd_ or _var/log/messages_ for Linux, using `journalctl -u docker.service`
