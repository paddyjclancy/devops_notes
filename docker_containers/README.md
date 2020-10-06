# Docker Terminal Commands

- `docker container run` - spin up a fresh container
- `docker container run -it <image> sh` - spins up new container and navigates terminal in (-it) for "interactive"
- `docker container start <ID>` - starts a specific container
- `docker container stop <ID>` - stops a specific container


- `Ctrl + P + Q` - exit container without terminating main process
- `exit` exit container AND terminating main process (sh)


- `docker container ls (-a)` - lists all containers currently running


- `docker container exec <ID> <COMMAND>` - executes command from outside the specified container


- `docker port <container name>` - shows port mappings within container


- `journalctl -u docker.service` - to read daemon logs in Linux
