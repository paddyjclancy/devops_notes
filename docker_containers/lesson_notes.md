##### Notes to be organised & assorted
### Big Picture
**Docker Enterprise Engine (EE)** - Engine, Ops UI and Ops on-prem registry
**Docker Community Engine (CE)** - Community edition of engine, contained API and Docker daemon

At lower OSI levels, these two engines are very similar. At the higher level, EE is far superior, and requires purchase.

### Docker Universal Control Plane (UCP)
###### See Docker documentation for installation / commands
- Operations GUI, installed as **containerised microservices app** on top of EE (on node), used for **visualisation**
- Utilises _Swarm_ for built-in protocols
- Control plane = manager nodes


### Docker Trusted Registry (DTR)
###### See Docker documentation for installation / commands
- Registries are where we store Images, securely (behind your own firewall)
- Utilises _Swarm_ for built-in protocols


### Role-Based Access Control (RBAC)
###### See Docker documentation for installation / commands
- Which users, have what level of access, to which objects
- Very important for enterprises
- EE supports this concept using a grant concept:
  - **Subject** - users
  - **Role** - permissions
  - **Collection** - resources
- Granularity is very powerful for RBAC, ie many different grants within the enterprise specifically designed for many roles.

### Image Scanning
###### See Docker documentation for installation / commands
- The primary means of defense against security flaws or insecure code within container images.
  - Image in this context refers to Docker Images (not JPEGs)
- Docker image security scanning is a process for finding security vulnerabilities within your Docker image files.
- Typically, image scanning works by parsing through the packages or other dependencies that are defined in a container image file, then checking to see whether there are any known vulnerabilities in those packages or dependencies.
- Coupled with pushing, this allows all images to be checked as and when they are being utilised.

### Layer 7 Load Balancing
###### See Docker documentation for installation / commands
- Layer 7 load balancing allows traffic going to host domains like 'acme.com' to be distributed across specific containers in your environment.
- With path-based routing, traffic headed to sub-domains within acme.com (eg. acme.com/app1 or acme.com/app2) can be separately routed to different sets of containers.
- This can be especially useful for optimizing application performance by driving different requests to different groups of containers.
- Layer 7 routing with Swarm is fully Docker native. It runs on Docker Swarm and routes traffic using cluster networking and Docker services, leverages Docker APIs, and is configurable via CLI and UI. It is also designed to be both scalable and highly available, meeting the needs of production applications.
