# Security regarding DevOps

### Areas of Risk Potential

1) Access Keys 
2) Passwords
3) Firewalls (AWS: Security Groups, NACLs)
3) IP Addresses

- When using key files / passwords in projects, they must be kept in a secure / enclosed location
	- Abstracted or hidden
		- Generally `.ssh/` in machine directories
		- Also use of `_password` method for variable definition / assignment in programs such as Python
		- If possible, encryption techniques such as hashing are encouraged.
			- Hashing ALSO improves memory management
	- No one who is surplus to requirement of particular scope should have access to these
	- They should NOT be in other machines / locations
		- Github
			- Github has built in notifications that will recognise potential security flaws
			- Also proper use of `.gitignore` to prevent accidental upload of sensitive info
		- EC2 instances 
			- External access may be possible due to insecure VPC set-up
	- Abstraction should be encouraged whenever possible
		- Eg. Terraform
			- Separation of Concerns / Interpolation of variables
			- We have so far used this for private IPs and VPC / AMI ids
			- Variable definition file is kept separate
	- Config files (`sshd_conf`) should be monitored to ensure appropriate levels of security
		- `PermitRootLogin`
		- `Password Authentication`
	- Use of `sudo passwd root` to set individual machine passwords, which are stored in `ansible/hosts` for reference
		- Abstracted from user
		- Used in tandem with SSH keys to provide two layers of access security

- AWS - EC2 - VPCs
	- When setting up components and respective rules, be very aware of exactly who is going to have access to what
	- Access key pairs provided by company
		- VERY SENSITIVE!
		- Do not send around
		- Can be kept in Ansible vault
	- Security Groups and NACLs especially
		- SG   = Instance level
		- NACL = Subnet level
			- In and Out rules
			- Default to block all
	- IGW connects VPC to internet and therefore outside world   <-- Be wary!
	- Route tables connect IGW to subnets					     <-- Be wary!
	- When using Jenkins server (or equivalent) for CI pipelines:
		- Only allow access to VALID Github (or equivalent) IPs	
			- Open meta data provided on their own platform

### Operations assigned with these areas of Risk

1. Creating machines with Ansible -> Use Ansible Vault
2. Private SSH keys should be added to .gitignore
3. Anything private such as passwords should be placed in .gitignore before pushing to GitHub
4. Security Groups and NACL's should have port 22 open only to your IP.
5. Dynamic IP variables should be kept in gitignore
6. Any form of credentials should be encrypted or ignored (Important!)

### Best practices with areas of risk and tools

1. Add any ssh private keys to .gitignore
2. Where using Ansible use the encrypted and password locked Vault
3. Keep an eye out for any GitGuardian notifications
4. When using software try to make use of encryption files and plugins
5. Do not push any files with passwords or credentials to github
6. GitHub repo's can be set to private if need be!


