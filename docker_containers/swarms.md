# Swarms

A Docker Swarm is a group of either physical or virtual machines that are running the Docker application and that have been securely configured to join together in a cluster.

Once a group of machines have been clustered together, you can still run the Docker commands that you're used to, but they will now be carried out by the machines in your cluster.

The activities of the cluster are controlled by a swarm manager, and machines that have joined the cluster are referred to as nodes.

- __Single-Engine Mode:__ Installing multiple single Docker instances separately, and work with them individually

- __Swarm Mode:__ Install instances together as a _cluster_, and work with them all together (orchestration)

- `$ docker swarm init` - creates swarm (requires at least one running instance)

There are two roles: _managers_ and _workers_.
  - Recommended to have 3, 5 or 7 managers

When creating a swarm, there will always be a _swarm leader_:
  - Will generate new root Certificate Authority (CA)
  - Will hold set of keys, used for connecting with new nodes (manager and worker sets).
  - `$ docker swarm join` - adds new node to the swarm, which will hold its own client certificate (ID, Swarm_ID, Role)
  - If leader fails, one of the (manager) _follower nodes_ will be elected the new leader

Autolock is a feature used to cut off swarms, it only concerns managers.
  - Prevents restarted managers from automatically re-joining
  - Prevents the accidental restoration of old copies
  - `$ docker swarm init --autolock` - autolocks new swarm
  - `$ docker swarm update --autolock-true` - autolocks existing swarm
  - - `$ docker swarm unlock` - unlocks swarm
