# VPC - AWS

- Virtual Private Cloud
- Concept allowing devs to create their own bubble networks within AWS
- SEE VPC DIAGRAM

## Set-up

1) AWS > VPCs > Create VPC
2) Name, IPv4 CIDR
3) Create subnets
	- Using VPC ID
	- Availabiltity zone
		- Common to make individual subnets across multiple zones
	- IP with /24
	- Public, private
4) Internet gateway
	- Attatch to VPC
5) Route table
	- Pre-defined exists - shell
	- Default = Main == Private
	- Rename, shape as req
	- Does not connect to internet, only VPC
	- Public
		- Connect to IGW
		- Associate to public subnet
	- Private = Default
		- Associate to private subnet
		- CONNECT TO IGW FOR SET UP ONLY
6) Security groups
	- Specific ports for specific groups
	- Different groups for each subnet
	- PRIVATE - DB
		- Inbound
			- Custom TCP - 27017 - SG Public
			- SSH - 22 - MY IP
				- Will be changed to Bastion Private IP
		- Outbound
			- All traffic
	- PUBLIC - WebApp
		- Inbound
			- SSH - 22 - MY IP
			- HTTP - 80 - 0.0.0.0
			- HTTPS - 443 0.0.0.0, ::/0
		- Outbound
			- All traffic
7) NACL
	- Defaults ALL TRAFFIC for inbound outbound.
	- Public:
		- Add Inbound:
			- Rule 100 - HTTP - ALL
			- Rule 110 - HTTPS - ALL
			- Rule 120 - SSH - MY IP
			- Rule 130 - Custom (ephemeral) - 1024-65535
		- Add Outbound:
			- Rule 100 - HTTP - ALL
			- Rule 110 - HTTPS - ALL
			- Rule 120 - SSH - MY IP
			- Rule 130 - Custom (ephemeral) - 1024-65535
				- Covers 27017 ie mongodb
		- Associate to Public subnet
	- Private
		- Add Inbound:
			- Rule 100 - Custom - 27017 - Public subnet
			- Rule 110 - Custom (ephemeral) - 1024-65535 - All IPs
			- Rule 120 - SSH - Public subnet
		- Add Outbound:
			- Rule 100 - Custom (ephemeral) - 1024-65535 - All IPs
			- Rule 110 - HTTP - 80 - ALL
			- Rule 120 - SSH - 22 - Public subnet


###### SEE VPC DIAGRAM


### Unable to resolve host ip?
- Private IP requires adding to localhost file
- `cd etc/`
- `sudo nano hosts`
- Add new line:
	- `127.0.1.1 ip-[PrivateIP]`


### Connecting Mongodb?

- Bad gateway error 502 can be fixed as such:

- Check for correct ip (private - DB instance):
	1) DB_HOST (in `$ env`)
	2) Provision file - export line 
	3) .bashrc

- Run npm instead of pm2 - more output for troubleshooting

## Bastion Server / Set-up

- One way in, one way out - very high security
- Abstracts high-security servers (MongoDB)
- Located in public subnet, exposed
- Holds single function

1) Switch off MongoDB server first from inside DB
	- `sudo systemctl stop mongod`
	- `service mongod status` <-- Check

2) Security groups - Private
	- Remove SSH access
3) Create public instance
	- New security group - Bastion
		- Inbound: SSH - My IP
		- Outbound: All Traffic 0.0.0.0
4) Append private (DB) security group
	-  Inbound: Bastion Private IP
5) scp key into Bastion
	- In new /.ssh folder
6) ssh into DB (using private IP), through bastion (using IPv4)
7) Start up mongodb server
	- `sudo systemctl start mongod`
	- `systemctl status mongod` <-- Check
8) Go to domain
9) Go to domain/posts


## Security Groups

- Operate on instance level
- Support allow rules only

## NACL - Network Access Control List

- Optional layer of security acting as a firewall, surrounding subnet
- Acts on subnet level
	- Broader than SGs, which work on instance level
	- Automatically applied to all instances of subnet
- Stateless
	- ie return traffic must be explicitly allowed in rules
- Need to specify both rules in and out
- Supports allow and deny
- Rules are ordered
- Include ephemeral ports
	- Short lived transport protocol port
	- aka Dynamic Ports
		- Used on a per request basis
	- First line provision.sh = update
	- Server reaches out to internet (on port 80)
	- Returning data
	- Ports 1024 - 65535
	- Needs to pass through NACL

## Deleting VPC

- Stop & terminate instances first