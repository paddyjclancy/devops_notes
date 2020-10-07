# Container Networking

###### Bridge Networking / Single-Host Networking
- Oldest, most common, least efficient
- Built-in, contains NAT
- Comprises of multiple containers in isolated 'islands', connected via a bridge.
- Mapping ports to host machine is the only way to cross these bridges

###### Overlay Networking / Multi-Host Networking
- Single layer 2 network spanning multiple hosts
- `$ docker network create` to create, and then attach
- Control plane is encrypted by default, data plane can be encrypted manually
- Currently container-specific

###### MACVLAN
- Every container has specific IP and MAC address
- All containers joined to 'single line' of the network
  - No port mapping
  - No bridges
- Requires promiscuous mode on host (not great for public cloud)


If using multiple networks on one host, there will always be a default

## Network Services

###### Service Discovery
- Every new service gets a name
- Names registered with Swarm DNS (every service)
- This makes all swarm services ping-able by name if being pinged from same network

###### Load Balancing - Ingress
- External clients can access node service ( / container) from any node in the swarm, even if it does not contain said service itself

###### Load Balancing - Internal
- From within network
