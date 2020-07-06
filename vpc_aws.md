# VPC - AWS

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
	- Default = Main
	- Rename, shape as req
	- Does not connect to internet, only VPC
	- Public, Private
6) Security groups
	- Specific ports for specific groups
7) NACL
	- Inbound
		- Rule 110 - SSH - MY IP
