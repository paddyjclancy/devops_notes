# Security Principles Regarding DevOps

### Key Areas of Risk

- SSH / Access Keys
- Passwords / Secrets
- Networking Permissions (Firewalls etc)
- IP addresses

These never want to be shared / moved to locations where they are not vital requirements, such as GitHub, or where access is insecure.

Access key pairs (especially those provided by a company) are VERY sensitive.
	- Do not send these around
	- Do not keep them in an insecure location
	- Use Ansible Vault service
	- Set as Environment Variables
	- Use `.gitignore`

Careful use of `.gitignore` and Ansible vaults (or equivalents) will assist as backup in maintaining a high level of internal security for these objects. as files.

Abstraction and interpolation of variables and tokens - eg IP addresses in Terraform - are a good method of removing sensitive information from main files. IE SEPARATION OF CONCERNS

GitHub will notify of any potential security flaws it notices, be aware of these

Encryption is another encouragable technique for protecting data
	- Eg hashing

#### AWS - VPCs

Good practices for network management:
	- Use of Bastion servers
	- Use strong firewalls, and allow only the minimum required access where possible
		- SGs - Instance level
		- NACLs - Subnet level
		- IGW - Opens VPC to the world
			- Be wary
	- If using Jenkins or equivalent for CI integration, ensure VALID IPs have been granted access
		- Can be found on company site meta data


  world
    |
    |
   \ /
   VPC - Internet Gateway
    |
    |
   \ /
  Network table
    |
    |
   \ /
   NACLs
    |
    |
   \ /
  Subnets
    |
    |
   \ /
Security Groups  
    |
    |
   \ /
EC2 instance


#### Useful links

Ansible Vault:
	- https://docs.ansible.com/ansible/latest/user_guide/playbooks_vault.html

Encryption:
	- https://www.howtogeek.com/howto/33949/htg-explains-what-is-encryption-and-how-does-it-work/

Environment Variables:
	- https://medium.com/chingu/an-introduction-to-environment-variables-and-how-to-use-them-f602f66d15fa

Network Strategy:
	- https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-network-and-security.html