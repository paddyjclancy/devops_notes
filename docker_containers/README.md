# Docker Terminal Commands


## Containers
- `$ docker container run` - spin up a fresh container
- `$ docker container run -it <image> sh` - spins up new container and navigates terminal in (-it) for "interactive"
- `$ docker container start <ID>` - starts a specific container
- `$ docker container stop <ID>` - stops a specific container
- `$ docker rm <ID>` - remove a halted container
- `$ docker build -t <name>` - builds container from Dockerfile and tags it with _name_ (-t / --tag)
- `$ docker run -d -p 3000:3000 <name>` - start a container and run an application
  - `-d` - runs the container in detached mode (in the background)
  - `-p 80:80` - map port 80 of the host to port 80 in the container


- `$ docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"` - creates an Ubuntu container, with a file `/data.txt`, containing a random number between 1 and 10,000:


- `$ docker container ls (-a)` - lists all containers currently running
- `$ docker container exec <ID> <COMMAND>` - executes command from outside the specified container


- `$ Ctrl + P + Q` - exit container without terminating main process
- `$ exit` exit container AND terminating main process (sh)


- `$ docker port <container name>` - shows port mappings within container


- `$  journalctl -u docker.service` - to read daemon logs in Linux


## Images
- `$ docker image pull <ID> (-a)` - pulls an image from registry to host
- `$ docker image inspect <ID>` - to show config and layers of an image
- `$ docker image rm <ID>` - deletes image


## Docker Repos and Pushing
With a free account, Dockerhub allows you to make unlimited Public repos, and ONE private.
- `$ docker login -u <username>` - log in
- `$ docker tag <ID> YOUR-USER-NAME/<tag-name>` - adds a custom tag
- `$ docker push YOUR-USER-NAME/<repo-name>` - pushes container into repo
