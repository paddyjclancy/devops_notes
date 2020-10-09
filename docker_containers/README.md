# Docker Terminal Commands


## Containers
- `$ docker container run` - spin up a fresh container
- `$ docker container run -it <image> sh` - spins up new container and navigates terminal in (-it) for "interactive"
- `$ docker container start <ID>` - starts a specific container
- `$ docker container exec ...` - to execute an internal container command from outside
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

- `$ docker node ls` - lists all docker nodes


## Swarms
- `$ docker swarm init` - creates swarm (requires at least one running instance) / exits single-engine mode

- `$ docker swarm init --external-ca ...` creates swarm using an external Certificate Authority


- `$ docker swarm join --token ...` - adds new node to the swarm. Specific command shown when using the following commands _in situ_:
  - `$ docker swarm join-token manager` - will provide token for command to add new nodes to a swarm (manager role).
  - `$ docker swarm join-token worker` - will provide token for command to add new nodes to a swarm (worker role).


- `$ docker swarm join-token --rotate worker` - provides token for converting a manager to a worker.

- `$ docker swarm join-token --rotate manager` - provides token for converting a worker to a manager.


- `$ docker swarm init --autolock` - autolocks new swarm

- `$ docker swarm update --autolock-true` - autolocks existing swarm

- `$ docker swarm unlock` - unlocks swarm


## Container Networking
- `$ docker network ls` - lists all current networks

- `$ docker network create <NAME>` - creates network in single command (bridge default)

  - `$ docker network create -d overlay <NAME>` - creates overlay network


- `$ docker network create -o encrypted` - ditto, but encrypted data plane

- `$ docker network inspect <NAME>` - to display details for specific networks

- `$ docker port <NAME>` - displays all port mappings within container


## Volumes
- `$ docker volume create <NAME>` - creates a volume

- `$ docker volume rm <NAME>` - delete volume

- `$ docker volume ls` - lists all available volumes

- `$ docker volume inspect <NAME>` - displays details for specific volume


- `$ docker container run -d -it --name voltest \` _`--mount source=ubervol, target=/vol alpine:latest `_ - mounts a volume to container
  - `source` = which volume
  - `target` = where to mount within container


## Secrets
- `$ docker secret create <NAME> <SOURCE>` - creates a secret using text contained within <SOURCE>

- `$ docker secret ls` - list all secrets

- `$ docker secret inspect <NAME>` - displays details only of specific secret (_NOT_ contents)


## Stacks
- `$ docker stack deploy -c stackfile.yml <NAME>` - deploys a full stack from the compose file, and assigns a name

- `$ docker stack services <NAME>` - returns list of all services, and details, held within a stack
