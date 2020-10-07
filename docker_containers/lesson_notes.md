# Notes to be organised & assorted


## Container Networking

Bridge Networking / Single-Host Networking
- Oldest, most common, least efficient
- Built-in, contains NAT
- Comprises of multiple containers in isolated 'islands', connected via a bridge.
- Mapping ports to host machine is the only way to cross these bridges

Overlay Networking / Multi-Host Networking
- Single layer 2 network spanning multiple hosts
- `$ docker network create` to create, and then attach
- Control plane is encrypted by default, data plane can be encrypted manually
- Currently container-specific

MACVLAN
- Every container has specific IP and MAC address
- All containers joined to 'single line' of the network
  - No port mapping
  - No bridges
- Requires promiscuous mode on host (not great for public cloud)


If using multiple networks on one host, there will always be a default


############################################################################

#### Persistance
Containers have so far effectively been 'Read Only'. Changes isolated to a removed container will be lost.

**Volumes** provide the ability to connect specific filesystem paths of the container back to the host machine.

Before your computer can use any kind of storage device (such as a hard drive, CD-ROM, or network share), you or your OS must make it accessible through the computer's file system. This process is called **mounting**.

If a directory in the container is mounted, changes in that directory are also seen on the host machine. If we mount that same directory across container restarts, we'd see the same files.

- Create a volume, using `docker volume create [Name]`
