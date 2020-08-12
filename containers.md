# Containerisation

###### See https://www.youtube.com/watch?v=TvnZTi_gaNc

### Virtual Machines

- Completely isolated from host and other VMs
	- Strong security boundaries
- Runs complete OS, including kernel
	- Require more resources
- Can run almost any OS
- Deployed using VM Managers eg VirtualBox
- Updates and upgrades need doing manually and regularly
- Uses Virtual Hard Discs for storage (single VM)
	- For multiple VMs, uses SMB file share
- Load balancing - VMs will move to other servers using failover clusters	
	- Multiple servers working together to maintain high availability
- VMs can fail over to another server in a cluster, with the VM's operating system restarting on the new server
- Uses virtual network adapters.

### Containers

- Lightweight isolation from host and other containers
	- Less strong security boundary
	- However can be improved
- Runs partial OS
	- Can be tailored to contain only the required services
	- Requires less resources
- Uses the same OS as host
- Deployed using **Docker** or orchestrators such as Azure Kubernetes Service
- Updates and upgrades done through updating build file (Dockerfile)
- Use Azure Disks for local storage (single node)
	- Azure Files (SMB shares) for multiple nodes / servers
- Containers do not move
	- Orchestrator can start or stop containers automatically on cluster nodes to manage load / availability
- If cluster node fails, containers within will be rapidly recreated on another cluster node
- Uses isolated view of virtual network adapter
	- Less virtualisation
	- Host firewall shared with containers