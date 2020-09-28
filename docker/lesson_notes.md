# Notes to be organised & assorted
A **Dockerfile** is simply a text-based script of instructions that is used to create a container image:

```
FROM node:10-alpine						# This image is not stored locally, so will be fetched
WORKDIR /app
COPY . .
RUN yarn install --production			# yarn is an alternative to npm
CMD ["node", "/app/src/index.js"]		# Specifies default command to run when starting container from image
```

- To build an image from the above Dockerfile, enter `$ docker build -t docker-101 .`
	- **Run this in the directory containing the Dockerfile**
- To start a container and run an application, enter `$ docker run -d -p 3000:3000 docker-101`
		- `-d` - run the container in detached mode (in the background)
		- `-p 80:80` - map port 80 of the host to port 80 in the container

- To see the ID of containers, enter `docker ps`
- To enter into a container, and do something with it, use `docker exec [ID]` `cat /data.txt`
- To stop a container using its id, enter `docker stop [ID]`
- Remove a halted container using `docker rm [ID]`


### Repos and Pushing
With a free account, Dockerhub allows you to make unlimited Public repos, and ONE private.

- Create public repo, named 101-todo-app

Applying a tag within terminal:

- Login using `docker login -u [username]`
- Apply tag using `docker tag docker-101 YOUR-USER-NAME/[tag-name]`
- Push container into repo using `docker push YOUR-USER-NAME/101-todo-app`

### Using Ubuntu (or other OS)
Containers can contain OS systems such as Linux Ubuntu. The following line of code creates an Ubuntu container, with a file `/data.txt`, containing a random number between 1 and 10,000:

`docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"`


#### Persistance
Containers have so far effectively been 'Read Only'. Changes isolated to a removed container will be lost.

**Volumes** provide the ability to connect specific filesystem paths of the container back to the host machine.

Before your computer can use any kind of storage device (such as a hard drive, CD-ROM, or network share), you or your operating system must make it accessible through the computer's file system. This process is called **mounting**.

If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

- Create a volume, using `docker volume create [Name]`
